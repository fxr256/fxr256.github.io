---
layout: post
title:  "The Trouble with Knowledge Transfers"
date:   2019-01-03 18:00:01 +0100
categories: working culture
---
Have you ever done a knowledge transfer? If so, how do you feel about it now?
Do you think it was helpful, that you achieved something? Or do you consider it
a waste of time?

Personally, I'm dissatisfied with the knowledge transfers I gave in the past. While I think I 
managed to transfer some knowledge, I'm quite sure that I didn't get the best end result for the
used time and effort. To clarify: When talking about knowledge transfers, I mean dedicated meetings
(usually an hour long) where some expert educates a number of participants about some topic. Usually, the
meeting is recorded and sometimes someone even listens to the recording. 
I think this is style of knowledge transfers should be avoided. Here are my reasons:
	
#### It Isn't Cost Effective
Meetings are very expensive in general as they consume the time of every participant. 
A meeting with five participants equals five person hours of lost time which is enough for a small feature.
Additionally, knowledge transfer meetings also require some kind of preparation. Depending on how
fragmented the knowledge is in your team and how aggressively you want to address this problem, 
you might end up with a large amount of these meetings. This can quickly become prohibitively expensive, 
especially if you often have new team members and/or new blocks of knowledge to share.

#### It Usually Comes at the Wrong Time
Knowledge transfers are often done in advance. Team members are informed about something which they might require
in the future but it is unclear when (or if). This is a problem as the transferred knowledge might already be
(partially) forgotten until it is needed.

#### It Is Often Shallow
Naturally, you cannot dive too deeply into a topic in a one hour session. So, the transferred knowledge might 
actually be too shallow to help in dealing with a customer issue or when extending a certain code area 
in the future. This could be fixed by spending more time on the session, but this makes them even more expensive.

#### It Addresses the Wrong Problem
A knowledge transfer intends to spread some information within the team. Usually, this is about obscure code
areas or complex functionalities of the product. The core assumption behind this is that the rest of team is
either unable to get an insight into this part of the code/product by themselves or that it would take an
unreasonable amount of time. From my point of view this is the core issue. 
Every part of your code/product should be easy to understand for a competent developer. You should have enough
automated tests and product specification at hand that it is possible to make changes to the code and that bugs
can be separated from features. This good practice eliminates the need for most knowledge transfer sessions by 
itself and pays off in other areas as well.

## What to Do Instead
I have already mentioned that good code, high automated test coverage, and a proper specification can largely
eliminate the need for knowledge transfers. For the remaining use cases, I propose using a wiki. Whenever you have
the feeling that you really should document something somewhere (and you cannot just rewrite the code to make
it clear), create a wiki page for this topic and write it down. Note that you should only write down what
**cannot** be learned from the source code. If you violate this rule, you will probably end up with wrong / 
outdated entries in your wiki as the code evolves at a different speed. However, it can be a good idea to 
include the entry point of a certain feature in the wiki to make it easier for you team members to actually find
it. By entry point I mean the package/class in the codebase where the feature is located. 

Using a wiki like this neatly gets rid of the timing and cost issues. Writing a wiki is less taxing than
preparing and holding a presentation. Also, people will only read a wiki entry if they really have to while 
the sheer existence of a meeting usually causes people to join it. A wiki entry which is never read only wastes
its creator's time while a pointless meeting wastes everybody's. As the entry can be read at any time, it is no
problem to quickly revisit it at some later point in time. While this is also true for a recorded meeting, 
it is much easier to find the information you are looking for in a wikipage.

I have mentioned above that knowledge transfers are often too shallow. Wiki entries can be as detailed as the 
creator wants them to be, but they probably shouldn't be too long. The key difference between the
wiki and the meeting is that the wiki only aims to give you the information you cannot get in the code. The
code is the true source of information and it can answer any of your questions. So, using wiki here does not
exactly solve the shallowness problem, as much as it just avoids it. 

That's all I have to say on the subject. I hope you can see my point even if you may not agree. If you know a 
different way to do knowledge transfers which solves the problems I have mentioned, please let me know.