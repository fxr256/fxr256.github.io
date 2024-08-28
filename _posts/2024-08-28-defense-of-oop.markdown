---
layout: post
title:  "In Defense of Object-Oriented Programming"
description: "It has become popular to condemn object-Oriented programming. In this blog post, I'll attempt to defend the practice."
date:   2024-08-28 17:26:01 +0100
categories: software design
---
It has been fashionable to condemn [object-oriented programming (OOP)](https://en.wikipedia.org/wiki/Object-oriented_programming) for a long time. The practice was already [proclaimed dead in 2006](https://kawagner.blogspot.com/2006/08/oop-is-dead.html), and the stream of [long critical articles](https://betterprogramming.pub/object-oriented-programming-the-trillion-dollar-disaster-92a4b666c7c7) and [silly tweets](https://x.com/Hasen_Judi/status/1815939219698974951) on the subject continues to this day. 

I understand that many developers are frustrated with OOP. I've criticized [the practice myself](https://thinkingsideways.net/software/design/futile-quest-for-true-oo.html), and I agree that OOP has failed to achieve its goals. However, it's a mistake to just discard OOP alltogether. When [done correctly and with a lot of restraint](https://thinkingsideways.net/code/sane-programming.html), it still offers some benefits. In this blog post, I want to point out the good things that OOP offers.

#### Defining OOP
But what exactly is OOP? This is a surprisingly difficult question to answer. Clearly, it's about objects, but what is an object exactly? [Alan Kay](https://en.wikipedia.org/wiki/Alan_Kay) is considered the inventor of the term, and [his definition](http://userpage.fu-berlin.de/~ram/pub/pub_jf47ht81Ht/doc_kay_oop_en) is as follows:
> I thought of objects being like biological cells and/or individual computers on a network, only able to communicate with messages (so messaging came at the very beginning – it took a while to see how to do messaging in a programming language efficiently enough to be useful).

Sadly, this definition isn't very helpful and also not in line with how OOP is actually done in reality. [Robert C. Martin](https://en.wikipedia.org/wiki/Robert_C._Martin) defines OOP like [this](https://x.com/unclebobmartin/status/1813946286808137787):
> OOP is the partitioning of systems into cohesive units composed of hidden data structures and exposed functions called through a separately defined dispatch table. 

Martin mentions three important points here:
1. Data and functions (=behavior) are combined in the same units.
2. The data is hidden while the functions are exposed.
3. The runtime behavior might change depending on the type of parameters passed to a function. The "dispatch table" he mentions is a mechanism for implementing [polymorphism](https://en.wikipedia.org/wiki/Subtyping).

This is a lot clearer than Alan Kay's vision. It's also important to note that while polymorphism is usually implemented via [inheritance](https://en.wikipedia.org/wiki/Inheritance_(object-oriented_programming)), this is not the only way to achieve this. For example, [Bjarne Stroustrup](https://en.wikipedia.org/wiki/Bjarne_Stroustrup) thinks that it's possible to [do OOP without inheritance](https://www.youtube.com/watch?v=xcpSLRpOMJM), as you can achieve polymorphism with [generic programming](https://en.wikipedia.org/wiki/Generic_programming) instead. Now, we're still not entirely sure what OOP means, as Martin, Stroustrup, and Kay define the term differently. Hence, I'll define the term myself. That way, we at least gain clarity in the context of this blog post.

My personal definition of OOP is that OOP is the combination of (mostly hidden) data and behavior in the same unit. That means a unit containing only behavior isn't object-oriented, and a unit with only data in it isn't object-oriented either. However, this is fine, as there is no rule that every piece of code in a codebase needs to be object-oriented. Instead, we can mix and match different paradigms as we see fit to achieve the best outcome. I included neither polymorphism nor inheritance in this definition, as I think that these techniques aren't that important. They can be useful in certain situations, but you can still do OOP without them. I also think that data hiding isn't essential. While the majority of data will be hidden, some might be exposed. I don't see why a unit should suddenly lose its "object-oriented" status just because we've made one piece of data public instead of private.

#### Reasons to use OOP
But why should we use OOP in the first place? I think that there are three advantages to using OOP:
1. It **can** be easier to understand than procedural programming.
2. It facilitates the creation of powerful data structures.
3. It facilitates writing automated tests.

Let's go through these points one by one. Object-oriented code can be easier to understand as it allows the hiding of unnecessary details. For example, a complex data structure like a thread-safe hash map is easier to use when all its implementation details are hidden. This is easy to achieve with OOP but much harder to do in procedural programming. For example, let's take a look at [this hash map implementation](https://web.archive.org/web/20160329102146/http://elliottback.com/wp/hashmap-implementation-in-c/), which is done in C. Notice how we have to pass a pointer to the map itself into functions like "hashmap_put". This is not needed when using OOP. In general, object-oriented data structures are very powerful and offer significant productivity gains. Also, through the use of generics, these complex data structures can also be used in a type-safe manner. This is very hard to achieve in a purely procedural language like C, as we need [to rely on macro commands](https://sglib.sourceforge.net/). Last, using OOP makes it easier to write automated tests as it is easier to replace unwanted parts with mocks. Passing a mock into a constructor is easy; manipulating the linker to achieve the same in a procedural language is much harder. Having a good suite of automated tests is a great way to [keep productivity up](https://thinkingsideways.net/testing/reasons-for-no-tests.html) during the development process. Hence, this is a big advantage.

These three advantages are the reason why I consider OOP valuable and usually pick it over procedural programming, with the exception of very small projects. There are other points that sometimes get listed as advantages of OOP, which I don't agree with. These are:
1. Increased reuse.
2. Greater flexibility to change your architecture.
3. The ability to model your code after the real world.

OOP has been around for decades, but reuse hasn't improved. The greater flexibility is mostly an illusion. Sure, we can switch our database implementation if we only interact with a wrapper, but how often do we actually do that? Also, there are a lot of hidden properties in our current architecture that we implicitly rely on. For example, we might discover that our new database is much slower in certain situations than our old one. The database wrapper, therefore, only offers the illusion of flexibility. Last, I don't believe that modeling your code after the real world is helpful. I've written more about this [here](https://thinkingsideways.net/reviews/ddd-book-review.html). Sadly, the three non-advantages were widely hyped during the rise and peak of OOP. This has tarnished the reputation of the practice.

The good news is that it's easy to reap the benefits of the actual advantages of OOP by [showing restraint](https://thinkingsideways.net/code/sane-programming.html). By avoiding inheritance, polymorphism, and design patterns, we avoid the complexity for which OOP is criticized. We end up with code that is object-oriented where it makes sense and procedural (or functional) where it offers no benefits. In a sense, we end up with the best of all worlds, and this can be very helpful in the [battle against complexity](https://www.quora.com/When-is-OOP-better-than-FP-and-vice-versa/answer/Aaron-Christianson-2).

#### Why are so many people mad about OOP?
I think part of the reason why some people are very vocal about hating OOP is that the technique was overhyped for a long time. This led to overblown expectations as well as a dogmatic usage of the paradigm. I've written about the [futile search for true OOP](https://thinkingsideways.net/software/design/futile-quest-for-true-oo.html) before, and I think that a lot of time was wasted on that endeavor. Sadly, it's impossible to give a full overview of all the reasons against using OOP here, both because it would take too much space and because I don't have full knowledge of all the things anybody has ever said against OOP. However, I found some recurring patterns during my research. OOP is ofter critized for:
1. failing to reduce complexity.
2. adding a lot of boilerplate because it adds a lot of indirection.
3. encouraging modeling after the real world even though this doesn't add any benefits.
4. scattering logic throughout the codebase.
5. encouraging the sharing of mutable state.

All of these points are valid. We will encounter these problems if we use OOP dogmatically and without restraint. This is the main problem of OOP: it makes it very easy to create a big mess. It's easy to get wrong and hard to get right. However, I still believe that it's beneficial [when done right](https://thinkingsideways.net/code/sane-programming.html) and in the right circumstances. We're doing ourselves a disservice when we condemn OOP entirely.

### Conclusion
OOP can be easier to understand, allows the construction of powerful data structures, and facilitates the writing of automated tests. We can avoid its downsides by avoiding inheritance, polymorphism, and design patterns. It is a mistake to condemn OOP in total just because of its past excesses.

If you liked this blog post, please share it with somebody. You can also follow me on [Twitter/X](https://twitter.com/fxr256).