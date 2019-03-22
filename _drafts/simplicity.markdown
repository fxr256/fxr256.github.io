---
layout: post
title:  "Respect Simple Solutions"
date:   2019-03-22 18:00:01 +0100
categories: code
---
From my observations, simplicity is not valued enough in software development. Instead, there is a lot of emphasis placed on flexibility. Many developers like to build a solution which handles any problem which might appear at some point in the future. In that regard, they are fortune tellers, trying to find a solution for eventual problems. This can work out very well if their predictions are right. Most of the time, however, this flexibility only causes unneeded complexity in the code which gets in the way and does not solve any future problems. This is not surprising as telling the future is a messy business. Nevertheless, this thinking is encouraged both at universities and in many corporate environments and in my opinion it is very dangerous. For example, a few years ago, I was asked by a colleague to change the if-else-statement I had just written into a switch-case-statement. I was confused as the code only had two different situations to handle and using a switch-case-statement seemed like overkill (I also despise switch-cases in general, but this is another matter). So, I asked him why I should change it and he told me that the expected further cases adding to the switch-statement in the future and wanted the code to be ready for it. He also dismissed my suggestions of leaving the if-statement for the moment and changing it to a switch-statement only when needed. He said that he wasn't confident that whoeever was going to do the change in the future was competent enough to recognize that the if-statement needed to be changed. In the end, I gave in and changed the code. The switch-case was not extended to this day. 

What my colleage at the time failed to realize is that flexibility does not come for free: You pay for it with increased code complexity. Flexibility usually implies more indirections in your code. More indirections mean that it becomes harder to figure out what happens where (and when) in your code base. If you add too much indirections in your code, you will spend a lot of time searching for code. This happens quickly if you use too involved object orientation in your code (deep inheritance hierarchies, many overridden methods, many design patterns). Also, some design patterns like the [visitor pattern](https://en.wikipedia.org/wiki/Visitor_pattern) are very powerful, but very hard to grasp from the code. 

Instead of striving for as much flexibility as possible, you should instead use the simplest solution which ticks all the boxes. What does this mean in terms of code? Let's look at an example. This example is based on a real piece of code taken from an enterpise cloud software. Naturally, I have changed the code to protect the innocent. It is a Java 7 code base (yes, these still exist). We have a `CitrusFruit` interface with two known implementations `Lemon` and `Lime`. Now, let's look at a snippet of code working with the interface and the two implementations:

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

So, what's happening here? We've got a list of citrus fruits which may contain any combination of limes and lemons as both of these implement the `CitrusFruit` interface. However, we have to separate the limes from the lemons as our store needs proper implementations. The predicate / filter combination solves this problem and is very flexible as we can pass in any implementation of `CitrusFruit`. However, it is also hard to understand, verbose and produces compile errors when compiled with javac - or warnings when compiled via the eclipse compiler -, due to the wild usage of generics. There is a much simpler way to solve this issue: 

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
{% endhighlight %}

This code compiles without errors, is shorter and trivial to understand. Of course, it is less flexible. Adding more types of citrus fruits requires additional handling. If the list of supported types becomes too long, we might have to use a different solution. However, for the moment, this solution is much better than the previous one. I don't know why the more verbose and flexibile solution was chosen. Whoever wrote the code probably had good reasons. Nevertheless, I know that no further subclasses of `CitrusFruit` was introduced in the 1.5 years. So, I'm quite confident that my solution will not become a problem due to its low flexibility in the forseeable future.

To wrap up: You should always strife for the least amount of flexibility in your code as more flexibility means more complexity. Keep in mind that [good design is imperfect design](https://www.youtube.com/watch?v=lY54TmmEllY) and that a good code base can easily be refactored if necessery. And if you like to dabble in fortune telling, maybe you should focus on future stock-prices instead. 
