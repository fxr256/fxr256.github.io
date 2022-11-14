---
layout: post
title:  "Book Review: Elegant Objects by Yegor Bugayenko"
description: "This blog post contains a review of Yegor Bugayenko's book Elegant Objects."
date:   2019-02-10 16:50:34 +0100
categories: reviews
redirect_from: /reviews/2019/02/10/elegant-objects-review
---
I like to read about software development. As you are reading a blog about this topic right now, chances are that you share the same hobby. However, there is so much material out there that it is hard to decide what to read. Today, I want to make this decision a bit easier by recommending a book: [*Elegant Objects*](https://www.goodreads.com/book/show/29326350-elegant-objects) by Yegor Bugayenko. You might be familiar with Yegor as he is a [blogger](https://www.yegor256.com/) himself. He is known for his strong and often polarizing opinions. One recurring theme of his blog is object orientation, more precisely, how to do it correctly. Yegor feels that how object orientation is done today is not how it should be done. He feels that [Alan Key's](https://en.wikipedia.org/wiki/Alan_Kay) vision wasn't achieved. So, he wrote a book about how to properly design objects. The book consists of 23 loosely related practical recommendations. Yegor has embedded links to related posts on his blog into the book. To give you a better impression of his ideas, I will link to these posts as well when appropriate.

In *Elegant Objects* Yegor talks about naming, object composition, error handling and anti-patterns. From my point of view, his opinion on object composition is the most interesting part of the book. Yegor strongly favors very small objects. For example, here is how Yegor creates a sorted list of all files in a directory (I have slightly changed the code for brevity. The original version can be found on page 142 of the book): 
{% highlight java %}
Collection<String> names = new Sorted(
	new Unique(
		new Capitalized(
			new FileNames(
				new Directory("myDirectory")
			)
		)
	)
);
{% endhighlight %}
Quite a polarizing style, isn't it? Depending on your preference, this code is either beautiful or horrifying. Yegor calls these mini-classes *composable decorators*. He claims that in true object oriented software the majority of the code has to look like this. In fact, he argues that there should not be any operators. Rather than an operator called `if` there should be a class named `If` which you use instead. Furthermore, the majority of the logic is moved into constructors. Yegor puts it like this on page 169:
> Objects are first-class citizens and their initialization through constructors is the software. Not operators or statements, but constructors.

What does this mean in terms of code? Here is an example from page 29:
{% highlight java %}
class Cash {
	private int dollars;

	Cash(float dlr) {
		this((int) dlr);
	}
	Cash(String dlr) {
		this(Cash.parse(dlr));
	}
	Cash(int dlr){
		this.dollars = dlr;
	}
}
{% endhighlight %}

The purpose of this class to encapsulate an amount of money. It stores the information in a private attribute of type `int`. However, there are consumers which have a different type at hand, namely `String` and `float`. In Yegor's opinion it is better to use constructors for this mapping rather than using utility classes. Also, he thinks that the more constructors of this style you have, the better, as your class will be more flexible. Following this style, you will end up with more constructors than methods.

Yegor's unorthodox opinions also include a strong aversion to [getter and setters](https://www.yegor256.com/2014/09/16/getters-and-setters-are-evil.html), [NULL usage](https://www.yegor256.com/2014/05/13/why-null-is-bad.html), [public constants](https://www.yegor256.com/2015/07/06/public-static-literals.html), [mutable objects](https://www.yegor256.com/2014/06/09/objects-should-be-immutable.html), [unchecked exceptions](https://www.yegor256.com/2015/07/28/checked-vs-unchecked-exceptions.html), [mocks](https://www.yegor256.com/2014/09/23/built-in-fake-objects.html) and [type casting](https://www.yegor256.com/2015/04/02/class-casting-is-anti-pattern.html). I think his argument against mocks is very interesting. Yegor correctly points out that mocking can result in very brittle unit tests. It is very easy to accidently break the mocks, because you change the used method in the class under test. In this case, you will end up with a failing test even though the class still works fine. Yegor's fix for this problem is to provide a fake object as part of each API / interface. As he wants each class to implement interfaces, he puts the fake implementation straight into the interface. Each unit test can just pass the provided fake into the class under test via the constructor. This way, you only have to change the provided fake if you modify the interface. However, the downside of this approach is that you end up with test code in production and a global fake object which is shared by all your tests. As you need to implement all methods of the interface in your fake and also need a powerful enough fake to power all your tests, you will often end up with a largish fake object. 

So, why do I think that this is a good book? I like that Yegor is not afraid to challenge the status quo. He believes in his style of object orientation and provides clear and hard rules. This is very refreshing, but obviously should be taken with a grain of salt. His advice makes me question the way I write code (especially in Java) and this is a good thing. Like Yegor, I believe in short methods and class, despise null and static methods, prefer tests over documentation and like immutable objects. I'm still on the fence regarding the usage of fakes and of composable decorators, but I will try them out in the future. The book's writing style is to the point and very readable, even though the sentences are a bit disconnected at times. However, it is an enjoyable read in total.

Of course, the book has flaws as well. First of all, it is way too expensive at $40.96. Obviously, Yegor can charge whatever he wants for his work, but I feel that this high price will hamper the spread of his ideas. In fact, I would've bought the book years ago, if it was cheaper and available as an e-book. Another downside is that some ideas in the book are too abstract, i.e. that they cannot be realized with today's languages (e.g. enabling lazy loading for immutable objects). I think the last thing the world needs are more programming languages, so I see little benefit in such abstract recommendations. Furthermore, Yegor sometimes uses very philosophical reasons to justify his programming style. For example, he argues that certain code styles should be used as they are more polite to the anthropomorphized object. I don't find this overly convincing as it seems constructed and forced to me. Last, there are some patterns which I don't agree with: Yegor recommends to only use checked exceptions and to always implement interfaces. I think he is wrong in both of these, but other readers might think differently.

All in all, I feel inspired by the book and if you are interested in learning a different take on object orientation and don't mind the high price, you should definitely read the book.