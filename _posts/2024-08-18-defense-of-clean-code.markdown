---
layout: post
title:  "Guest Post: In Defense of Clean Code"
description: "The book classic Clean Code has been viciously attacked recently. While it is not perfect, the main criticism is unfounded"
date:   2024-08-10 11:26:01 +0100
categories: software design
---
It seems to have become very fashionable to attack [Robert C. Martin’s classic book "Clean Code"](https://www.goodreads.com/book/show/3735293-clean-code). Lots of developers
voice their displeasure at the book and the bad practices it supposedly encourages on social media (as an example of
countless others, please see [this](https://x.com/ryanrwinchester/status/1762180771018686569) post on Twitter/X) and
very harsh criticism of it can also be found in blog posts and at conferences. One example would be the otherwise very
[thoughtful talk](https://www.youtube.com/watch?v=CDcP5e7-NOU) of David Whitney at Copenhagen DevFest, in which
Whitney even encourages listeners to burn their copies of "Clean Code".

I am by no means a blind follower of Robert C. Martin, or the ideas expressed in "Clean Code". Indeed, if a new
developer were to ask me today which book he should read, I would probably recommend [John Ousterhout’s excellent "A
Philosophy of Software Design"](https://www.goodreads.com/book/show/39996759-a-philosophy-of-software-design) rather than "Clean Code".

Still, the criticism of "Clean Code" seems overly harsh and strangely focused on one supposed piece of advice in it:
writing lots of small classes. The internet is ripe with developers venting their frustration about the atomized
codebases they are forced to work with, and David Whitney also criticizes "Clean Code" for encouraging needless
abstraction and dogmatism (ironically, one of the book recommendations in his talk is [Mark Seemann’s "Code That Fits in Your Head"](https://www.goodreads.com/book/show/57345272-code-that-fits-in-your-head) which I consider not only a massive waste of time but a much better example of dogmatic coding rules).

The thing is, I completely agree with the arguments against tiny classes. It can be incredibly frustrating to start
searching for a certain functionality in a promising-looking class and only finding it after checking six other classes
that don’t even seem related. Indeed, after working with a codebase where no class was bigger than maybe twenty lines –
this limit was rigorously enforced by one developer – I have gained a new understanding of the antipathy some developers
feel for object-oriented programming.

Today, if a malicious genie gave me the choice between working with a 3000-line class or with the same functionality
split into 100 classes with 30 lines of code each, I would probably pick the former. Huge classes are bad for a lot of
reasons, but at the very least it is easy to find the right file, and the search function of your editor will often
quickly locate the relevant section within it. The same cannot be said for a completely atomized codebase where the
pieces are simple, but you can never see the whole picture.

So, how does "Clean Code" fit into this? Did it cause this wave of tiny classes that seems to have swept over the
industry (or at least over social media)? The best way to answer this question is to look at the text itself. This part
is often missing from the discussions both online and offline, and this oversight is one reason why these debates are
frequently unproductive.

We will start with functions. While they are not brought up as often, tiny functions have similar downsides as
tiny classes, and the chapter about functions is written by Robert C. Martin (unlike the one dealing with classes), so
we can hear it from the man himself. All quotes are from my 2012 edition of "Clean Code". On page 34, Martin writes:

> The first rule of functions is that they should be small. The second is that they should be smaller than
> that. (…)
> Every function in this program was just two, or three, or four lines long. Each was transparently obvious.
> Each told a
> story. And each led you to the next in a compelling order. That’s how short your functions should
> be!

It seems obvious that this advice could motivate programmers to write very short functions (even to a fault), but we
should not forget the qualifications Martin adds to his statement. Having a clear and compelling order with such tiny
functions is not easy, and most codebases consisting of tiny functions probably ignore this point. Still, this section
could reasonably be used to blame "Clean Code" for a developer’s arsenal of miniscule functions. So, what does the book
say about classes? The relevant chapter is written by Jeff Langr and has this to say about the size of classes on page
136:

> The first rule of classes is that they should be small. The second rule of classes is that they should be smaller than
> that. No, we’re not going to repeat the exact same text from the Functions chapter. But as with functions,
> our immediate
> question is always "How small?"

Langr then goes on to talk about the [single-responsibility principle (SRP)](https://en.wikipedia.org/wiki/Single-responsibility_principle), cohesion, and other classic object-oriented
programming rules that help limit class size and often result in many small classes. So, at this point, it looks like
the criticism is correct after all, and "Clean Code" can be blamed for at least some of the atomized codebases out
there.

However, this is not the end of the book. When we go to the "Emergence" chapter (also written by Langr), we can find
this section on page 176:

> Minimal Classes and Methods
>
> Even concepts as fundamental as elimination of duplication, code expressiveness, and the SRP can be taken too far. In
> an
> effort to make our classes and methods small, we might create too many tiny classes and methods. So this rule suggest
> that we also keep our function and class counts low.
>
> High class and method counts are sometimes the result of pointless dogmatism. Consider, for example, a coding standard
> that insists on creating an interface for each and every class. Or consider developers who insist that fields and
> behavior must always be separated into data classes and behavior classes. Such dogma should be resisted and a more
> pragmatic approach adopted.

This perfectly captures the problems created by blind adherence to the earlier rules, and I could not agree more with
Langr’s statement. So, whoever is using "Clean Code" to justify a codebase of five-line classes has either not read the
book at all or skipped the "Emergence" chapter. Indeed, I consider it likely that developers coding this way are
influenced by much older ideas like the SRP and are on a [quest for true object-oriented
programming](https://thinkingsideways.net/software/design/futile-quest-for-true-oo.html). They use "Clean Code" as a fig
leaf for their already existing taste and to deflect criticism of their coding style. After all, it is much harder to
object to the notion of "clean" code than to the object-oriented programming paradigm, which had its detractors ever since its birth.

On the flip side, developers who do not like tiny classes or unnecessary abstractions now think "Clean Code" caused this
coding style. As a result, they often attack the book and are wary of anyone who claims to follow its advice. This is
understandable, however, it is both misinformed and harmful to their cause, as it focuses the discussion on the book
rather than the coding style. So, one might say that this is a big misunderstanding and a symptom of a larger conflict
inside software development.

Still, it does not mean Robert C. Martin, Jeff Langr, and the other authors of "Clean Code" did everything right. They
should have known better than to include the far too broad statements regarding class and function size. While the arguments
against very long classes and functions are valid, going this far in the opposite direction is harmful as well, and
although they added the necessary caveat to balance out their advice, this section is in a different chapter and can be
missed unless the book is read cover to cover. I am convinced Martin et al. never intended to encourage atomized
codebases, but their book made it easy to be misunderstood. This is one reason why I consider "Clean Code" to be largely
superseded by the mentioned "A Philosophy of Software Design", which takes great care to avoid such mistakes.

Still, "Clean Code" is a classic and raised a lot of important points back in its day. I am glad to have read it in 2012
and think people can still learn from it today, especially when it comes to proper naming of variables and functions. It
certainly does not deserve the vitriol spewed online, especially since it does not even say what its critics claim it
does.

## Conclusion:

"Clean Code" is not advocating mindless abstraction, even if some sections of the book can be read this way when taken
out of context. While there are better books for beginners today, the hate against it is largely a sign of a bigger and
more important conflict inside software development: the [proper use of abstraction](https://thinkingsideways.net/software/design/cost-of-abstraction.html). We should talk about this issue
directly instead of debating a book most people taking part in the debate haven’t even read.

If you liked this blog post, please share it with somebody. You should also have a look at the many blog posts from the
main author. As for me, you can find me on [Twitter/X](https://twitter.com/Geisterschleier).