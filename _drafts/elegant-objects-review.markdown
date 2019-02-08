---
layout: post
title:  "Book Review: Elegant Objects by Yegor Bugayenko"
date:   2019-01-03 18:00:01 +0100
categories: reviews
---
I like to read about software development. As you are reading a blog about this topic right now, chances are that you share the same hobby. However, there is so much material out there that it is hard to decide what to read in our limited spare time. Today, I want to make this decision a bit easier by recommending a book: [Elegant Objects](https://www.goodreads.com/book/show/29326350-elegant-objects) by Yegor Bugayenko. You might be familiar with Yegor as he is a [blogger](https://www.yegor256.com/) himself. He is known for his strong and often polarizing opinions. One recurring theme of his blog is object orientation, more precisely, how to do object orientation correctly. Yegor feels that how object orientation is done today is not how it should be done. He feels that [Alan Key's](https://en.wikipedia.org/wiki/Alan_Kay) vision wasn't achieved. So, he decided to write a book about how to properly design objects. At its heart, *Elegant Objects* is a book about object orientation. The book consists of 23 loosely related practial recommendations. 

In *Elegant Objects* Yegor talks about naming, object composition, error-handling and anti-patterns. He strongly favors small objects with multiple constructors. For example, here is how to write create a list of sorted file names of a directory:
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
Quite a polarizing style, isn't it? Depending on your preference, this code is either beautiful or horrifying. Yegor calls these mini-classes *composable decorators*. He claimes that in true object oriented software, the majority of the code has to look like this. In fact, he argues that their should not be any operators. Rather than an operator called `if` there should be a class named `If` which you could use instead. The majority of the logic is moved into constructors. Yegor puts it like this:
> Objects are first-class citizens and their *initialization* through constructors *is* the software. Not operators or statements, but constructors.
Yegor's unorthodox opinions also include a strong aversion to getter and setters, NULL usage in any form, public constants, mutable objects, unchecked exceptions, mocks and type casting. I think the point he makes against mocks is very interesting. 