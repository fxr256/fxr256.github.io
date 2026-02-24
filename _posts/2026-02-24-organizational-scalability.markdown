---
layout: post
title:  "Organizational Scalability"
description: "Software companies should prepare for success by adopting good organization scalability. This blog post gives some recommendations on how to do it."
date:   2026-02-24 09:26:01 +0100
categories: people
---
When developers talk about scalability, we're chiefly referring to technical scalability. In other words, we want to enable our systems to gracefully handle growing loads. This is a technical problem, and as with most technical problems, it's well understood and manageable. However, there's a related problem that is primarily a people problem: organizational scalability. This topic is rarely explored, which makes it worthy of its own blog post.

In the context of this blog post, organizational scalability is defined as the ability of our organization to gracefully handle growing success. This includes having more customers, a higher market share, more employees, and everything else that comes with it. Technical scalability is a subset of organizational scalability, as it's also only relevant when we're successful. After all, if nobody uses our software, we don't need to worry about our servers getting overloaded.

Even though organizational scalability is only relevant when we're successful, that doesn't mean that it's a luxury problem. Insufficient organizational scalability can significantly slow down our growth. As growth is king in the software industry, any loss of momentum can be a serious threat to our business. So, how can we prepare for success on an organizational level in the context of software development? I was fortunate enough to experience sustained success and growth during my time with SuccessFactors and hence have a few recommendations.

It's important to stress that these recommendations are only for established companies! If we're still unsure whether the company will survive at all, then we need to focus on the basics: find our market and get enough cash flow. Only once we've established ourselves and started to see some early signs of success should we think about our organizational scalability.

Furthermore, I only recommend practices that are also beneficial to small development teams. It would be ridiculous to implement something like [SAFe](https://framework.scaledagile.com/#big-picture) in a small team just because we might need it ten years down the road. With that out of the way, let's dive into the recommendations in detail.

#### Prepare For New Hires
Success increases demand for software developers, as more customers mean more feature requests and support tickets. The natural fix for this is to hire more people. It's expected that growing the team will decrease [productivity at first](https://en.wikipedia.org/wiki/Brooks%27s_law). However, we expect this to turn around after a couple of months. 

Sadly, this turnaround isn't guaranteed, so we need to hire good people and help them get up to speed quickly. First, we need to come up with a way to screen applicants to ensure that we find good candidates. While the team manager will do most of the work in that area, at least some developers should be involved in the hiring process to ensure cultural fit and to help filter out any weak candidates. 

After we have hired someone, we need to be prepared for him to show up. That means having the necessary hardware at hand, knowing what access rights he will need and how to get them, and, most important of all, a plan on how to get him up to speed. This plan also includes picking out some introductory work items for him. In my experience, small, low-priority bugs are perfect for this.

I highly recommend appointing a dedicated mentor for every new colleague. The mentor serves as the primary point of contact to answer any questions that the new hire might have. Good documentation is also very helpful for new hires, which leads me to my next point.

#### Have Good Documentation
As growth means both bigger teams and more capable software, it becomes increasingly difficult to manage information. It gets harder to keep everyone up to date and to keep everything important in mind. As a result, [good documentation](https://thinkingsideways.net/processes/documentation.html) becomes essential. It pays off to invest time into documentation early on and to keep the documentation up to date, as it allows everyone on the team to independently hunt down needed information. This is not only very efficient but also removes a lot of friction in distributed teams where asking a colleague might not always be an option. Documentation also helps to retain knowledge. Some employee churn is expected over time, and with comprehensive documentation, we can at least mitigate the brain drain that comes with people leaving.

In addition to writing good documentation, we should properly describe any bugs or features in our issue tracker to make it easy to understand the requirements and the context. I've written about this best practice already in more detail [here](https://thinkingsideways.net/processes/issue-tracker.html).

#### Have Some Processes
Even when we're very small, I highly recommend having some lightweight processes in place. My recommendation would be [Kanban](https://thinkingsideways.net/processes/kanban.html), but anything can work. I think it's important to have some kind of weekly planning meeting to make sure that we're aligned on what to do next. We also need an issue tracker where everything we're currently working on is visible. This way, we can keep track of who's doing what and easily check on the progress.

We should have a couple of meetings each week to discuss the current state. In these meetings we talk about the current state using the issue tracker as guidance. The general idea is to quickly resolve any blockers and to share knowledge about what the rest of the team is working on. Note that the idea is to focus on the tracker and not on the person! If I haven't done any work that's in the tracker, then I just keep quiet. That's a notable difference compared to a standard Daily Scrum meeting and the key factor why these meetings deliver value in contrast to most Daily Scrums.

It can be tempting to just go without any explicit processes when we're a very small team. This can also work, especially if the team members have already worked together in the past and know each other's quirks. However, this way of working doesn't scale as the information flow is too limited. It also struggles to quickly onboard new colleagues for the same reason. Hence, my advice is to have some processes from the start. Even very lightweight ones can carry us for a long time.

#### Keep Regressions Low
Customers expect our software to work. Hence, we need to be very careful not to introduce regressions. This is especially problematic when we're delivering our software as a service because this usually means that all (or at least most) of our customers get upgraded to a new version at the same time. If we ship a version with a couple of regressions in it, we will receive feedback very quickly and spend the next couple of days shuffling customer tickets and hammering out a fix. Needless to say, this is a poor use of our time and a loss for everyone involved. 

If we keep pushing out buggy versions, then the customers we fought so hard to acquire might very well leave and move to a competitor who respects their time. Few companies are able to lock in their customers so tightly that leaving is close to impossible, and even for those companies, low software quality is not a good look. Customer churn is very damaging to a company as it disrupts expected revenue streams and because the cost of acquiring new customers is often very high. 

For all these reasons, we should see every regression as a personal failure that should never happen again. We need to understand why it happened and what we can do to prevent it from happening again. I also highly recommend making new features or changes to old ones opt-in. That way, the customer has to actively turn them on instead of receiving a potentially unwelcome surprise from us. Keeping regressions in check requires discipline, but I'm convinced that it pays off in the long term.

#### Learn From Customer Tickets
Customer tickets can tell us a lot about what's wrong with our product. We should use them to figure out which areas of the product aren't working well and what exactly causes frequent customer problems. For example, if we often see issues that are caused by a misconfiguration of the software on the client's side, it's an excellent idea to add further validations and to give better user guidance in the configuration. This helps us to keep our maintenance load under control. 

Also, if we frequently encounter data corruption issues, it's not enough to just fix the corruption and move on. Instead, we need to figure out where exactly these corruptions are coming from and address the root causes. Over time, it should become harder and harder to cause any kind of data corruption in our software.

#### Automated Tests
Automated tests are a great way to keep our productivity up, as they prevent fixed bugs from creeping back into the product. As successful products often live for a long time and continuously get more complex, they benefit massively from a comprehensive automated test suite.

Hence, we should get started with automated testing early and keep investing in it over time. [I usually recommend sticking to unit tests](https://thinkingsideways.net/testing/integration-tests.html), but integration tests can be very useful in the early stage of a product when the internal structure isn't sufficiently clear yet. We need to find the right mixture for our product and situation. An unbalanced test suite can actually reduce productivity, so it's important to get it right and to keep an eye on it. Unstable and very slow tests can massively reduce productivity and need to be tackled quickly.

Having no automated tests at all is certainly a bad idea, as manual tests have no return on investment. It is fine to only test manually when we're just getting started, but as soon as we start earning money with our software and plan to expand, we need to start writing automated tests.

#### Embrace Subsidiarity
In a very small team it's possible for one leader to make all decisions. However, as we grow, this is no longer an option, as simply too many decisions need to be made. Instead we need to rely on the [subsidiarity principle](https://thinkingsideways.net/processes/subsidiarity.html) and delegate the decisions to the people best equipped to make them. Research has shown that this delegation leads to better results. It's essential for big software development organizations, as coordinating many different teams from top down doesn't work.

We should strive to build a bottom-up culture from the very start. Otherwise, we might teach our colleagues not to think for themselves and not to share their perspective. Obviously, this is the exact opposite of what we want. For bottom-up to work, people also need the courage to decide things on their own. With the wrong company culture this will never work.

### Conclusion
We can improve organizational scalability by preparing for new hires, having good documentation, having some lightweight processes, keeping regressions low, learning from customer tickets, writing automated tests, and embracing subsidiarity.

If you liked this blog post, please share it with somebody. You can also follow me on [Twitter/X](https://twitter.com/fxr256).