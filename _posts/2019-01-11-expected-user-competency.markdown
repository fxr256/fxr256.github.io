---
layout: post
title:  "What's Your Expected User Competency?"
description: "This blog post introduces the concept of the expected user competency which you should consider in your software and UI design."
date:   2019-01-11 22:35:01 +0100
categories: software design
redirect_from: /software/design/2019/01/11/expected-user-competency
---
During the years of my work in software development, I have noticed that each software needs a certain level of
competency to be used properly. Some pieces of software are extremely easy to use, usually because the problem they
solve is very easy as well. However, some software is clearly aimed at experts or power users and less competent uses
will have a hard time using it. I call this the expected user competency (EUC) of software. A software with a
high EUC is the text editor [Vim](https://en.wikipedia.org/wiki/Vim_(text_editor)). Vim is extremely powerful, but it
is so hard to use that most novice users can't even figure out how to close the program. In fact, over [one million
people](https://stackoverflow.blog/2017/05/23/stack-overflow-helping-one-million-developers-exit-vim/) needed to look
up how to quit Vim on Stack Overflow. The creator of Vim expected the users to either be familiar with
its predecessor or to be willing to invest some time into learning to use the program.

Another example of a high EUC is the versioning control software [Git](https://en.wikipedia.org/wiki/Git). Git is a
distributed version control system and was primarily created for the development of the Linux kernel. Thus, its user
group were Linux kernel developers in general and Linus Torvalds in particular. It is quite natural to assume that
Linux kernel developers are familiar with shell-based programs and are somewhat used to cryptic argument flags. Also, it
is normal for developers in  the open source world to disagree with each other. Git makes it very easy to fork a
repository, make changes to it and to send your changes back to the original repository. The main owner (in case of
Linux: Linus Torvalds) can then decide whether your changes should be included in the repository at all, whether they
need to be revised first, or whether they can be included the way they are. As many Git users disagree on the right way
to use the program (e.g. small vs. big commits, rebases vs. merge commits, reset vs. revert), there are many ways to
achieve the same thing and commands to turn a change done by another developer into your preferred style. All of this
power makes Git more complicated to use than traditional central source code control programs like
[SVN](https://en.wikipedia.org/wiki/Apache_Subversion). Hence, Git has a higher EUC. Switching from SVN to Git is not easy
and I've personally seen how much chaos this can cause in a commercial development project.

The EUC concept is not limited to tools. It is also relevant for programming languages and for (G)UIs. For example,
Python has a much lower EUC than C as it hides a lot of the technical details from its user. There is no need to
think about memory management and buffer overflows in Python while it is crucial in C. GUIs express
their level of EUC mainly by how powerful they are, i.e. how much is happening on the screen. There are a lot
of business UIs with a very high EUC. Let's look at an example:
![UI image](/images/complexUI.png)
Beautiful, isn't it? And this is only the very first page of this UI (there are three more down below). In case you 
are wondering, this UI is a custom SAP program which allows you to check whether you have missed any days in your
logged work. It interacts with SAP's Cross-Application Time Sheet (CATS) and is obviously very powerful. 
I'm sure that there a lot of great reasons why it looks the way it does, but a different UI with a lower EUC might be
more suitable for most of the users as this is an employee self service use case.

So, what does this all mean? I want to stress that having a high EUC is **not always wrong**. If you know your user base well and
you know that they will be able to handle the complexity, then there is nothing to worry about. In fact, some  problems
are impossible to solve in an easy manner. A high EUC only becomes a problem if the assumptions about the user base turn
out to be wrong. Git was intended for distributed open-source development done by very tech-savvy users. Now, it used as
well in commercial development where a lot of the programs features are irrelevant while its complexity remains
the same. This is not a fault of the Git developers, as they never intended their software to be used in this manner.
However, it illustrates how important it is to think about the EUC of a product when making the decision to use it.
Rather than using Git, something like [Mercurial](https://en.wikipedia.org/wiki/Mercurial) or even a centralized source
code control system like SVN might be a better choice for many companies. Whenever you decide to use something,
think about the core audience of this software and figure out whether you are part of it. If you are, chances are that
you will be able to handle the EUC. If not, you should take a look at how hard to use the software is and then make an
informed decision.

On the flip side, you should always try to keep the EUC of your software as low as possible. Even if your core target
audience is highly skilled, keeping the EUC low will keep you prepared for a bigger audience in the future. Also, it
will help you find the simplest possible solution for the problem. This is especially important when designing
GUIs and APIs. An API which requires a lot of knowledge about your internal data model is fine for internal usage, 
but will be hard to use for any external users (and will probably leak details which you don't want to expose). So,
the next time you have a moment, reflect on your EUC and see whether you are happy with it. If you liked this blog post, please share it with somebody. You can also follow me on [Twitter/X](https://twitter.com/fxr256). 