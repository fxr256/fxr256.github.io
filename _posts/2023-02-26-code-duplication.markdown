---
layout: post
title:  "Code Duplication: When It Makes Sense to Repeat Yourself"
description: "While code duplication is often harmful, it can be beneficial in the right circumstances."
date:   2023-02-26 10:00:01 +0100
categories: code
---
In programming, code duplication is considered a sin while code reuse is considered a virtue. However, reality isn't as black and white and today I'm going to explain why code duplication can be a good thing in certain situations. But first let's briefly recap why code duplication is considered a bad practice. Three reasons come to my mind:

- Maintenance: If you have duplicate code in your codebase, maintaining and updating it becomes more difficult. When you need to make a change, you have to do it in multiple places, which increases the risk of bugs and inconsistencies.

- Brain overload: Duplicate code can make your codebase  harder to understand. It can also create confusion if the multiple copies of the code are slightly different as it will be unclear which version of the code should be used.

- Waste of time: Recreating already existing code is a waste of time and resources. 

These are good reasons to aim for as much code reuse as possible. However, there is more to this story. All of these reasons depend on a certain context. Writing duplicate code only wastes time if you're unaware that you're duplicating code in the first place. As long as you know that you're duplicating code, you can just copy and paste it, so your time investment will be minimal. Also, code duplication only makes maintenance more difficult if the two copies *actually need to be kept in sync*. If it doesn't matter whether they behave exactly the same, then there is no problem. For example, imagine a simple utility class called "packager" which splits a list of objects into multiple packages of a certain size. If I copy this class from one repository into another one and later change the default package size in the new copy, then the original class can stay unchanged. It is not required that all copies stay in sync in such a basic use case. As I separated the two copies by placing the new copy in a different repository, brain overload is minimized.

With that out of the way, here are some situations in which code duplication can be helpful:

- Rapid prototyping: When you need to quickly test an idea, duplicating code can help you move faster without having to refactor the existing code first to enable reuse.

- Specific use case: If a piece of code is only needed for a specific use case, it may make sense to duplicate it instead of creating a generic solution that would add unnecessary complexity. [In general, it is often a good idea to choose a simple solution over a flexible one](https://thinkingsideways.net/code/simplicity-over-flexibility.html).

- Modularization: Code duplication can help to improve modularization as you can duplicate a certain class instead of having a compile dependency between two modules.

- Legacy code: If you are working with legacy code, duplicating a piece of code that is difficult to change can help you build new features without breaking existing functionality.

While most of these points are easy to understand, I want to add some more details to the "modularization" point. Let's imagine that I want to further modularize my codebase by moving some code into a new module. To do that, I need to define an API layer for the new module and move all existing users of the soon to be moved code to the new APIs. Once this is done, I can move the code and as a result isolate the concrete implementations from the outside. Let's revisit the "packager" class example from earlier. What should I do if the "packager" class is one of the classes which I want to move into my new module? I could define an API for it and switch any existing users to the API. This is fine if the target module is a platform module, but what if it is an application module and a platform module uses this code? This would violate my layering rules as platform modules shouldn't depend on application modules. Also, does it really make sense to add a dependency to another module just for a utility class? In this situation, it can be the best solution to just copy the "packager" class to each module which requires it. This way, dependencies between the modules are minimized and as the different copies don't have to be kept in sync, the code duplication isn't harmful. Having multiple copies of such a class in the codebase can be slightly confusing, but this is somewhat mitigated as the copies are in different modules.

### Conclusion
Code duplication is a bad practice, but in certain situations it can be the right thing to do. It depends on the context whether code reuse or code duplication is better. If you liked this blog post, please share it with somebody. You can also follow me on [Twitter/X](https://twitter.com/fxr256).