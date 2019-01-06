---
title:  "Knowledge transfers don't scale"
date:   2019-01-03 18:00:01 +0100
categories: working culture
---
Have you been ever asked to do a knowledge transfer? If yes, how do you feel about it now?
Do you think it was helpful that you achieved something when doing it? Or do you consider it
a waste of time?

Personally, I'm dissatisfied with the knowledge transfers I gave in the past. While I think I 
managed to transfer some knowledge, I'm quite sure that I didn't get the best end result for the
spend time and effort. To clarify: When talking about knowledge transfers, I mean dedicated meetings
(usually an hour long) where some expert tells a number of participants about some topic. Usually, the
meeting is recorded and sometimes someone even listens to the recording. 
I think this is style of knowledge transfers should be avoided. Here are my reasons:
	
#### It isn't scalable
Meetings are very expensive in general as they consume the time of every participant. 
A meeting with five participants equals five person hours of lost time, which is enough for a small feature.
Knowledge transfer meetings are even worse as they also require some kind of preparation. Also, depending on how
segmented the knowledge is in your team and how aggressive you want to address this fact, you might end up with a 
large amount of these meetings. It is obvious that this doesn't scale, especially if you often have new team members
and/or new blocks of knowledge to share.

#### It usually comes at the wrong time
Knowledge transfers are often done in advance. Team members are informed about something which they might require
in the future, but it is unclear when (or if). This is a problem as the transfered knowledge might already be
(partially) forgotten until it is needed.

#### It is often shallow
Naturally, you cannot dive too deeply into a topic in an one hour session. So, the transferred knowledge might 
actually be too shallow to help in dealing with customer issue or when extending the code area in the future. 
This could be fixed by spending more time on the session, but this makes them even more expensive and most of 
the time this is a too costly investment.

#### It addresses the wrong problem 
A knowledge transfer intends to spread some information within the team. Usually, this is about obscure code
areas or complex functionalities of the product. The core assumption behind this is that the rest of team is
either unable to get an insight into this part of the code/product by themselves or that it would take an
unreasonable amount of time. From my point of view this is the core issue. 
Every part of your code/product should be easy to understand for a competent developer. You should have enough
automated tests and product specification at hand that it is possible to make changes to the code and that bugs
can be separated from features. This good practice elimantes the need for most knowledge transfer sessions by itself
and pays off in other areas as well.

## What to do instead
I have already mentioned that good code, high automation test coverage and a proper specification can largely
elimnate the need for knowledge transfers. For the remaining use cases, I propose using a wiki. Whenever you have
the feeling that you really should document something somewhere (and you cannot just rewrite the code to make
it cleared), create a wiki page for this topic and write it down. Note that you should only write down what
*cannot* be pulled from the source code. If you violate this rule, you will probably end up with wrong / 
outdated entries in your wiki as the code evolves at a different speed. However, it can be a good idea to 
list the entry point to a certain feature in the code to make it easier for you team members to actually find
it. 

Using a wiki like this neatly gets rid of the timing and scalabilty issues. Writing a wiki is less taxing than
preparing and holding a presentation. Also, people will only read a wiki entry if they really need to while 
the sheer existence of a meeting usually causes people to join it. A wiki entry which is never read only wastes
its creator's time while a pointless meeting wastes everybody's. As the entry can be read at any time, it is no
problem to quickly revisit it at some later point in time. While this is also true for a recorded meeting, 
it is much easier to find the information you are looking for in a wikipage.

I have writte above that knowledge transfers are often too shallow. Wiki entries can be as detailed as the 
creator wants them to be, but they probably shouldn't be too long anyway. The key difference between the
wiki and the meeting is that the wiki only aims to give you the information you cannot get in the code. The
code is the true source of information and it can answer any of your questions. So, using wiki here does not
exactly solve the shallowness problem, as much as it just avoids it. 

That's all I have to say on the subject. I hope you can see my point even if you may not agree.