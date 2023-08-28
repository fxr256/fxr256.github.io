---
layout: post
title:  "Code Reviews Should Be Optional"
description: "Mandatory code reviews are ineffective, confusing and slow everything done. Hence, reviews should be optional."
date:   2023-03-12 10:00:01 +0100
categories: processes
---
Mandatory code reviews are very common in commercial projects. While the idea to increase code quality by reviewing code changes is sound, I want to make a case for abolishing mandatory code reviews and to replace them with optional ones. But before I explain this, let's talk about code reviews in general.

There are shallow and deep code reviews and the two kinds are fundamentally different: 
- In shallow code reviews the reviewer just takes a superficial look at the code changes and checks whether anything is glaringly wrong. The code is not executed and it isn't checked whether it actually fulfills the underlying requirements. This review style is cheap to do, but only finds obvious issues. It is also quite good at sparking arguments about different preferences in coding style (e.g., whether static imports should be used) which is not very helpful and irrelevant in the grand scheme of things. Sadly, these kinds of discussions are [very popular debate subjects](https://en.wikipedia.org/wiki/Law_of_triviality). One last downside of shallow code reviews is that they don't work well on huge code changes as it very difficult to understand the changed behavior by just looking at the dozens of changed files. Also, only few reviewers have the patience to skim over so many files. 

- Deep code reviews are much more involved than shallow ones. Here the reviewer first understands the problem that the code author wanted to solve. If the code belongs to a new feature, this includes understanding the requirements and thinking about how they could be implemented. Then, he reviews the code changes in his local dev environment and runs the new code to see if it works. He thinks about whether the author's solution is the best one or whether some other approach would be even better. Also, he checks whether automated tests were written and whether they cover all relevant cases. By doing all this, he's *partially repeating* the author's work. Deep code reviews can find all sorts of issues, but they are very expensive. For this reason, they tend to be rarely used. If a development team is very busy, it might even be impossible for them to do deep code reviews because there is no capacity.

I'm under the impression that few people are aware of this distinction and hence expect deep review benefits from shallow code reviews. Now, with this out of the way, let me I explain why I think that reviews should be optional.

Mandatory code reviews have these disadvantages:

- Mandatory reviews make it impossible to distinguish between desired and enforced reviews. Often, developers know that their code changes are fine, but sometimes they would like another colleague to take a look. Most likely, they want a deep review in that case. If all code changes require a review, it becomes more difficult to tell these two use cases apart.

- If there are a lot of changes, the mandatory code review process can become a bottleneck. This can be very demotivating, especially for small code changes where the author wouldn't have requested a review voluntarily. In that case, he is blocked due to the process and has to find something else to do in the meantime. 

- If code reviews are mandatory, a lot of them have to be done. As time is limited, this will incentivize developers to do shallow code reviews which add very little value. It is better to use this time for fewer, but more valuable, deep code reviews. 

- Mandatory reviews raise wrong expectations in management. Management will be surprised that bugs slip through the cracks even though code reviews are done. What they don't realize is that the process itself makes code reviews less effective by pushing for shallow reviews.

- Mandatory reviews show a lack of trust in the developers' skill level and can be considered micromanagement.

Rather than doing mandatory code reviews, I strongly encourage using optional deep code reviews. Here, the code author voluntarily asks another colleague to take a deep look and to share his insights. This is especially helpful for junior colleagues and a great opportunity for them to grow. And because it is voluntary, it is less awkward in contrast to mandatory reviews which can become quite unpleasant if developers start arguing about minor details on GitHub. Code reviews can cause friction, especially if you have very different coding styles in your team. Hence, it is wise to only do them if they are welcome and add value.

Some readers might be worried about code quality at this point. After all, if no one is reviewing code, how can we make sure that it is good code? Well, we need to keep in my mind that by making reviews optional, we only get rid of shallow code reviews. As these are very superficial, they can be replaced with static code checks. Tools like [Sonar](https://www.sonarsource.com/), [Checkstyle](https://checkstyle.org/) and [SpotBugs](https://spotbugs.github.io/) are much better at finding such problems than any human: They are cheap, they are fast and you don't spend time arguing with them. Deep code reviews will still take place to handle very difficult changes and to guide new team members.

### Conclusion
Code reviews only add value if they are deep code reviews. Making them mandatory is harmful and should be avoided. Optional code reviews can be a great way to spread knowledge in your team and to make developers grow. If you liked this blog post, please share it with somebody. You can also follow me on [Twitter/X](https://twitter.com/fxr256).