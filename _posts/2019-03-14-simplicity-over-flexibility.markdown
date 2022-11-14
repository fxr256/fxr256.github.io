---
layout: post
title:  "Choose Simple Solutions Over Flexible Ones"
description: "This blog post explains why you should strive to keep your code simple. It explains what 'simple' means in this context and includes a real life code example."
date:   2019-03-24 16:47:01 +0100
categories: code
redirect_from: /code/2019/03/24/simplicity-over-flexibility
---
In my experience, simplicity is not valued enough in software development. Instead, there is a lot of emphasis placed on flexibility. Many developers like to write code which handles any problem which might appear at any point in the future. In that regard, they are fortune tellers, trying to find a solution for eventual problems. This can work out very well if their predictions are right. Most of the time, however, this flexibility only causes unneeded complexity in the code which gets in the way and does not actually solve any problems. This is not surprising as telling the future is a messy business. Nevertheless, this thinking is encouraged both at universities and in many corporate environments and, in my opinion, it is very dangerous. For example, a few years ago, I was asked by a colleague to change the if-else-statement I had just written into a switch-statement. I was confused as the code only had two different cases to handle and using a switch-statement seemed like overkill. So, I asked him why I should change it and he told me that he expected further cases in the future and wanted the code to be ready for it. He also dismissed my suggestion of keeping the if-statement for the moment and changing it to a switch-statement only when needed. He said that he wasn't confident that whoever was going to do the change was competent enough to recognize that the if-statement needed to be replaced. In the end, I gave in and changed the code. The switch-case was not extended to this day. 

What my colleague failed to realize is that flexibility does not come for free: You pay for it with increased code complexity (and with pointless switch-statements). Flexibility usually implies more indirections in your code. More indirections mean that it becomes harder to figure out what happens where (and when) in your code base. If you overdo it, you will spend a lot of time hunting for certain pieces of code. For example, you might wonder why a numeric value on your UI is wrong. You can quickly find out which method the frontend uses to read it from the backend. However, finding the piece of code which actually calculates this value can be much more difficult. I once had to navigate through ten classes to find the calculation logic for such a value. It was not a pleasant experience.

This kind of complexity overload happens quickly if you use too involved object orientation (deep inheritance hierarchies, many overridden methods). Also, some design patterns like the [visitor pattern](https://en.wikipedia.org/wiki/Visitor_pattern) are very powerful, but very hard to understand. 

Instead of striving for as much flexibility as possible, you should instead use the simplest solution which ticks all the boxes. What does this mean in terms of code? Let's look at an example. This example is based on a real piece of code taken from an enterprise cloud software. Naturally, I have changed the code to protect the innocent and to make it easier to digest. It is a Java 7 code base (yes, these still exist). We have a `CitrusFruit` interface with two known implementations `Lemon` and `Lime`. Now, let's look at a snippet of code working with the interface and the two implementations:

{% highlight java %}
  List<CitrusFruit> citrusFruits = getFruits();

  fruitStore.stockFruit(Lemon.class, new ArrayList<>(
          (Collection<? extends CitrusFruit>) Collections2
              .filter(citrusFruits, new CitrusFruitClassPredicate(Lemon.class))));

  fruitStore.stockFruit(Lime.class, new ArrayList<>(
          (Collection<? extends CitrusFruit>) Collections2
              .filter(citrusFruits, new CitrusFruitClassPredicate(Lime.class))));
}
{% endhighlight %}

This code uses Google's [Guava API](https://github.com/google/guava) to support functional programming styles on Java 7. [Collections2](https://google.github.io/guava/releases/14.0.1/api/docs/com/google/common/collect/Collections2.html) accepts a [predicate](https://google.github.io/guava/releases/14.0.1/api/docs/com/google/common/base/Predicate.html) to filter a list. The predicate looks like this:
{% highlight java %}
public class CitrusFruitClassPredicate implements Predicate<CitrusFruit> {

  private Class<?> clazz;

  public <T extends CitrusFruit> CitrusFruitClassPredicate(Class<T> clazz) {
    this.clazz = clazz;
  }

  @Override
  public boolean apply(CitrusFruit citrusFruit) {
    if (clazz == null || citrusFruit == null) {
      return false;
    }

    return clazz.isInstance(citrusFruit);
  }
}
{% endhighlight %}

`FruitStore` has this method signature and **only** accepts concrete implementations.
{% highlight java %}
  public <T> void stockFruit(Class<T> type, List<T> fruits)
{% endhighlight %}

So, what's happening here? We've got a list of citrus fruits which may contain any combination of limes and lemons as both of these implement the `CitrusFruit` interface. However, we have to separate the limes from the lemons as our store needs concrete implementations. The predicate / filter combination solves this problem and is very flexible as we can pass in any implementation of `CitrusFruit`. However, it is also hard to understand, verbose and produces compile errors when compiled with javac - or warnings when compiled via the eclipse compiler -, due to the wild usage of generics. There is a much simpler way to solve this issue: 

{% highlight java %}
  List<CitrusFruit> citrusFruits = getFruits();
  List<Lime> limes = new ArrayList<>();
  List<Lemon> lemons = new ArrayList<>();
  for (CitrusFruit citrusFruit : citrusFruits) {
    if (citrusFruit instanceof Lime) {
      limes.add((Lime) citrusFruit);
    }
    if (citrusFruit instanceof Lemon) {
      lemons.add((Lemon) citrusFruit);
    }
  }
  fruitStore.stockFruit(Limes.class, limes);
  fruitStore.stockFruit(Lemon.class, lemons);
{% endhighlight %}

This code compiles without errors, is shorter and trivial to understand. It is also less flexible: The loop cannot handle any new implementations of `CitrusFruit` by default. If the list of supported types becomes too long, we might have to use a different solution. However, for the moment, this solution is much better than the previous one. I don't know why the more flexible solution was chosen, whoever wrote the code probably had good reasons. Nevertheless, I know that no further subclasses of `CitrusFruit` was introduced in the past 1.5 years. Hence, I'm quite confident that my solution will not become a problem due to its low flexibility in the foreseeable future.

To wrap up: You should always strife for the least amount of flexibility in your code as more flexibility means more complexity. Keep in mind that [good design is imperfect design](https://www.youtube.com/watch?v=lY54TmmEllY) and that a good code base can easily be refactored if necessary. And if you like to dabble in fortune telling, maybe you should focus on future stock (or Bitcoin) prices instead. 
