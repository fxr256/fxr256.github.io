---
layout: post
title:  "Book Review: Domain-Driven Design by Eric Evans"
description: "This blog post contains a review of Eric Evans's book Domain-Driven Design."
date:   2023-02-05 13:50:34 +0100
categories: reviews
---
As the topic of domain-driven design (DDD) recently came up at my current job, I decided to get more familiar with the topic by reading Eric Evan's book ["Domain-Driven Design: Tackling Complexity in the Heart of Software"](https://www.goodreads.com/book/show/179133.Domain_Driven_Design). This was a mistake. Reading the book not only failed to convince me that DDD is worth the effort, it also was a terrible experience. So, I decided to write a blog post about the book to at least get something out of it.

Before I start to explain why I was so dissatisfied with the book, let's first briefly talk about what DDD actually is. It is a design philosophy which uses the domain as inspiration for designing software. The domain is the part of the real world where your software is supposed to solve a problem. For example, when building a bookkeeping software, bookkeeping is your domain. When using DDD you create a model of the domain and then use this model as guidance in your implementation. The idea is that code and model are aligned with each other so that changes to the code also change the model and vice versa. However, not everything in your code will exist in the model as large parts of the code have no counterpart in the real world. The underlying assumption is that this mental exercise will make your code better and improve communication between the developers and the customers / domain experts. DDD is highly linked with object-oriented programming. In fact, it cannot be used with a purely procedural language like C. The whole concept of DDD sounds lot like yet another [futile quest for true object-orientation (OO)](https://thinkingsideways.net/software/design/futile-quest-for-true-oo.html) to me. With that out of the way, let's critique the book itself. There are three big flaws in it:

#### Length
The book is more than 500 pages long. The length is padded by a lot of UML diagrams and frequent repetition of a few key points. Also, a significant part of the book is a listing of DDD implementation patterns which doesn't add a lot of value. The book would be much better if it was half the size which would still be enough to explain what DDD is and how to use it properly.  In general, I don't mind long books if their length is justified by the additional content. Sadly, this isn't the case here.

#### Writing style
While writing style is subjective in novels, this is a non-fiction book and we have to measure it on whether or not it manages to explain its key points. The book does a poor job here and I think the main reason for this is the overly complicated and pretentious writing style. Let's look at a couple of examples to illustrate this:

>Chapter 15, “Distillation,” discusses how to make distinctions within the domain layer that can unencumber the essential concepts of the domain from peripheral detail.

This example from page 97 nicely illustrates how unnecessarily complicated the writing style is. Words like "unencumber" and "peripheral" are out of place in a technical book which also targets non-native speakers. Another example for this pretentious style can be found on page 82:

>MODEL-DRIVEN DESIGN discards the dichotomy of analysis model and design to search out a single model that serves both purposes.

A word like "dichotomy" serves no purpose here except making the text harder to read. At times, the book reminds me of philosophical texts which also often struggle to express anything clearly. This also fits to the last two quotes I want to present here. The first one is taken from page 81:

>Defining objects that capture concepts of the domain seems very intuitive on the surface, but serious challenges are lurking in the shades of meaning.

I wasn't aware that there are different shades of meaning. This kind of flowery language should've been removed by the editor. My last example is this completely unhelpful definition in the glossary:

>domain: A sphere of knowledge, influence, or activity.

With that out of the way, let's move to the last big flaw.

#### Bold claims without proof
The book likes to make bold claims without providing any empirical evidence to back them up. This starts with the subtitle of the book which promises to tackle complexity in the heart of software. This implies that software following the DDD philosophy is less complex than other software which serves the same purpose. However, there is no proof for this in the book. Here's another bold claim (page 47):

>Projects that have no domain model at all, but just write code to fulfill one function after another, gain few of the advantages of knowledge crunching and communication discussed in the previous two chapters. A complex domain will swamp them.

Sadly, it is never explained what exactly a complex domain is and how being "swamped" affects a project. The idea that only projects following DDD can deal with a complex domain seems laughable to me, especially because the vast majority of code out there doesn't follow this philosophy. Interestingly, the author clearly states on page 76 that DDD is not suitable for all projects:

>Domain-driven design pays off best for ambitious projects, and it does require strong skills. Not all projects are ambitious. Not all project teams can muster those skills.

Again, it is not explained what qualifies as an ambitious project. Anyway, I think you get the idea. The book likes to state how great DDD is, but failed to convince me.

### Conclusion
So, where does this leave us? I've shown why I dislike the book and I wouldn't recommend it to anybody. However, there was one interesting section in the book. On page 57, Evans points out that you expose your underlying model to the user when he interacts with the software. If the model used in your software doesn't match the user's model, then confusion is created. He gives a concrete example of this: In old versions of [Internet Explorer](https://en.wikipedia.org/wiki/Internet_Explorer) bookmarks were stored as files. This meant that all the restrictions on filenames also applied to bookmarks. Hence, when a user tried to save a bookmark with a title which contained a character not allowed in files, he would get an error message stating that this character wasn't allowed in file names. Of course, the user wasn't aware that he was creating a file in the first place and hence confused. This is a good point which we should keep in mind, especially when designing APIs. **Everything which we expect the user to directly interact with should match his model.** Sadly, this is the only thing I learned. As a whole DDD seems overly complex and outdated to me. It seems like an idea fueled by the object-oriented programming hype of the 90s and early 2000s. [As I've mentioned before](https://thinkingsideways.net/software/design/futile-quest-for-true-oo.html), OO has not delivered and we should stop chasing this pipe dream.

Let me end this post by saying that I don't want to pick on Mr. Evans or belittle his work. I just want to give any potential reader an idea on what to expect from the book. If you're still interested in the topic of DDD after this post, you might want to check out the [free book "Domain Driven Design Quickly"](https://www.infoq.com/minibooks/domain-driven-design-quickly/). It is also poorly written, but quite short, and also conveys the central ideas of DDD. That concludes this blog post. If you liked it, please share it with somebody. You can also follow me on [Twitter/X](https://twitter.com/fxr256).