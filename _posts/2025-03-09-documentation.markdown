---
layout: post
title:  "The Software Documentation Trifecta"
description: "Software documentation targets developers, managers and customers. This blog post explains how to craft helpful software documentation for all three groups."
date:   2025-03-09 07:26:01 +0100
categories: processes
---
Even though most people will probably agree that software documentation is important, the topic of how to do it best is quite underdiscussed. I want to rectify this by offering some suggestions on how to do it. 

First, I think it's helpful to split the topic of software documentation. From my understanding, there are at least three different kinds of software documentation:
1. Documentation primarily targeting **developers** (e.g., code comments, internal wikis, style guides)
2. Documentation primarily targeting **management** (e.g., issue tracker entries, project plans, release schedules)
3. Documentation primarily targeting **customers** (e.g., setup guides, detailed feature documentation, best practices)

There's some overlap between these different kinds of documentation. For example, a developer might take a look at the customer documentation to understand how to configure a certain feature. That said, it's important to keep the primary target group in mind. The documentation needs to match their needs first, and any additional concerns are less important. Let's discuss the three different kinds in more detail.

#### Developer Documentation
Developer documentation is the most discussed kind of documentation. Usually, these discussions center around whether or not to add code comments. While this topic is out of scope for this blog post, I have addressed it in passing [here](https://thinkingsideways.net/code/clean-code.html). Instead of rehashing the topic, I want to stress that code comments are not enough. Not only does the code itself have to be readable, we also need a place for all the additional information a developer needs. This includes information like how to use the development toolchain, how to get code into production, what style guides to follow, where to find what in the codebase, etc. Basically, everything a new developer needs to know to be productive should be documented somewhere. Preferably, all this information should be in one place. My recommendation is to use some sort of wiki for this and include a link to this wiki in the "readme" files of each GitHub project. This way, every developer should at least know that the central wiki exists and hopefully should then be able to find whatever he needs in it.

#### Management Documentation
It's clear that management also needs certain pieces of information to do their job. For example, it needs answers to questions like:
1. When will which feature be shipped?
2. Which features currently in production absolutely have to be delivered?
3. Is anything at risk?
4. What is the bottleneck (a.k.a. critical path) for a certain feature?
5. Are we on track?
6. What kind of changes have we made to certain features over the years?
7. Why did we build that feature in the first place? Which customer is relying on it, and for what?
8. Are any teams overloaded or underloaded?

These needs cover project management concerns, people management concerns, and feature concerns. These differing needs make management documentation very challenging to do right. The hardest part is keeping track of feature changes. For example, imagine we're building a time management application, and we want to figure out why we added support for multiple overlapping time accounts. We might still remember that this was done a couple of years back but not why. We can probably find the relevant issue tracker entry by looking through the commit history of the changed code. However, it's far from guaranteed that this will include any information about the motivation. If we're lucky, we might learn that the feature was introduced to fulfill the special needs of a key customer. That's helpful but still doesn't tell us whether the customer is actually using the feature and what problem it's solving exactly. That kind of information is probably buried in some email account if it exists at all.

The key challenge here is to bind the different information threads together. In other words, we need to decide on a leading knowledge platform where all the information is stored and find a way to bind them to code changes. From my point of view, the only suitable choice for this is our issue tracker, as it maps directly to code changes. In general, I think that issue trackers are great communication tools. I've explained this [here](https://thinkingsideways.net/processes/issue-tracker.html) in more detail. That means that we need to spend more effort on our issues. More precisely, we need to include at least this information:
1. What is the motivation for this issue? Who needs it, and for what?
2. Is this a change to an existing feature? If yes, then we need to include a link to the last related issue so we can build a chain of changes.
3. When was this issue shipped / when do we plan to ship it?
4. What's the priority of this change?
5. What team is this assigned to?
6. Does it belong to any long-running project? If yes, we need to link to the project itself so we can get the full picture.

As we can see, this strategy only works if we get as much information into the issue tracker as possible. We can also link to other places, but the issue tracker has to be the central point that ties everything together. Only then can we link a code change to the bigger picture and get all the information we might need. However, this also means that there will be a lot of information to process. While digging through different lengthy issues is time-consuming, I still think that it's worthwhile as we can retain a lot of institutional knowledge this way, which otherwise might get lost. In addition to the issues themselves, we also have to construct suitable dashboards to cover the project management and people management concerns. When using this strategy, everybody is using the issue tracker, so the differing needs of engineers, product owners, and managers need to be met.

Whether or not a feature is actually used in production is something we cannot tell from the issue tracker. While getting this information is very difficult in traditional on-premise software, it's quite possible to figure it out in cloud software. Ideally, we should be able to check this with minimal effort in some kind of monitoring tool.

#### Customer Documentation
Great customer documentation is highly beneficial as it helps to prevent customer issues and makes the software easier to implement, which in turn [makes it more valuable](https://thinkingsideways.net/product/design/easy-implementations.html). Hence, we need to take great care when writing it. The most important thing to keep in mind is to always offer context. It's not enough to just describe how to configure a feature; we also need to give some explanation on what a feature actually does and why we might want to turn it on. Enterprise software often has very niche features that target certain highly specific scenarios. The customer has to be able to tell from the documentation whether or not he needs a certain feature. It's also helpful to use cross-references between different topics. For example, when describing how to enable overlapping time accounts in a time management system, it's a good idea to add a link to the time account section. Without context, the documentation will feel disjointed. 

Similar to the other documentation types, we also need a single place to tie all of our customer documentation together. In addition to the general documentation, we might have more specialized ones like descriptions of best practices, lists of important new features, or guides on how to solve common issues. All of this information needs to be gathered in one place so that the customer can actually find it. After all, even the best documentation is useless if it remains unread.

### Conclusion
Software documentation targets developers, managers, and customers. These three groups have different needs that need to be considered. However, they have the common need of a central point where they can find all documentation relevant to them.

If you liked this blog post, please share it with somebody. You can also follow me on [Twitter/X](https://twitter.com/fxr256).