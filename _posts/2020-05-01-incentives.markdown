---
layout: post
title:  "The Power of Incentives"
description: "This blog post talks about the incentives in the context of software development. Incentives are very powerful and hence must be managed carefully."
date:   2020-05-01 17:26:01 +0100
categories: processes
redirect_from: /processes/2020/05/01/incentives
---
Working in a corporation exposes you to a plethora of business processes. At their heart, these
processes are supposed to guide you into correct and appropriate behavior. They incentivize certain
behaviors and discourage others. But what if a process sets the wrong incentive? Take the yearly
bonus for example. The idea behind it is simple: Employees are supposed to work harder and make
better decisions as they can directly participate in the company's success. However, this idea falls
flat if employees are able to game the system. For example, some investment bankers were able to
realize profits early while pushing the accompanying risks into the future. As the bonus system only
considers the past year, they could maximize their salaries this way. They were incentivized to
value short term profits over long term ones. Naturally, the mid and long-term profits are more
important to the company, so the employee and the company have conflicting goals.

What are some examples of harmful incentives in the software industry? One example is the separation
of development and maintenance. This anti-pattern is especially common in custom development and
consulting work where a team of developers builds software for a customer who then handles the
deployment and maintenance. However, it can also be found in in-house development: The primary
development team might be overloaded with work and therefore a second team jumps in to do the
necessary development work for a new feature. After development is complete, the new feature is
handed over to the primary team and the auxiliary team focuses on other things. The issue with this
separation of concerns is that it incentivizes being fast over building quality software. As the
developers building the software won't have to maintain the software, they will cut corners if they
are feeling under pressure. Sadly, automated tests and clean code are often regarded as
non-essential which greatly harms the maintainability of the product in the long run. It is very
likely that time pressure will occur, because these kind of software projects tend to be time boxed
and that quality will suffer as a result. In addition to code quality, knowledge transfers will
probably be lackluster in this situation for both in-house projects and customer facing ones. In a
customer project, communication between the development team and the customer is often not clear
enough. In an in-house project, the primary development team has limited time to onboard the
auxiliary team and the auxiliaries won't have much time to do an extensive hand-over after they are
done as they have their regular duties to get back to. Also, the lack of up-front training makes it
very likely that the auxiliary team will have a steep learning curve. Of course, this doesn't mean
that every project following this pattern is doomed from the start. If all contributing developers
care about maintainability and if they have enough time, the software can turn out just fine.
However, I think this is a rare exception.

Another similar anti-pattern is having a dedicated test team. Separating quality control from the
developers sets the wrong incentive as it gives the impression that quality is someone else's
problem and that developers don't have to test their code. It also leads to communication issues as
often the testers don't quite understand what the code is supposed to do. Then, they have to get in
touch with the developers and ask them, which is annoying for all parties involved. Things get even
worse if the development team and the test team are not co-located. As testing is considered a
rather easy task, many companies outsource the task to low cost countries. Spreading development and
testing over multiple continents and different time zones makes this process even more inefficient.
If the testers find errors, they have to communicate them back to the developers and any fixes the
developers do in response need to get tested again which in turn requires another communication
cycle. There is also another problem: As the test team's primary task is to do manual testing, they
will be hesitant to automate. After all, a machine runs the automated tests and by automating more
and more of their work they'd effectively become obsolete. If the number of raised defects is
tracked in any way, they will raise as many defects as possible even if it might just be a
misunderstanding. Clearly, this is also inefficient. From my point of view, the only way to get a
decent quality software product is to put the testing (and the maintenance) into the hands of the
development team. This way, the developers have the incentive of writing quality software as they
will have to test and maintain the software themselves. Also, they will strife to write automated
tests as their testing competes with all of their other tasks. I think having a dedicated test team
should be avoided completely.

Next, let's talk about the complexity of software development processes and its impact. In a
start-up, processes concerning software development are often limited to some light-weight form of
issue tracking (e.g. in GitHub) and a very simple continuous delivery pipeline. Sometimes the
developers are even able to directly commit to the master branch, because they are trusted not to
break anything. This is great, but it doesn't scale. In a large development organization with
hundreds of coders working on more or less the same product, more rules need to be in place to
prevent complete chaos. The goal here is to bring some order to the plethora of code changes done
every day. As every code change has the inherent risk of breaking some previously working part of
the software, larger companies only want code changes which are "necessary" and "approved". Ideally,
the commits should be in relation to a feature in development or a bugfix for a known problem. "
Rogue" commits which deal with neither of these are usually not welcome. Hence, the developers are
supposed to jump through additional hoops before coding. Maybe they have to file a JIRA artefact for
every bug they want to fix, maybe they have to get approval for certain changes first, maybe some
changes are completely forbidden at certain points in time. In essence, all of these processes
incentivize developers to make fewer changes to the code. The
more red tape is required to make a "legal" change, the fewer changes will be made. While this can
be desired by the management to keep an overview about the made changes, it is not a good thing. The
only way new features can be developed and bugs can be fixed is by making code changes. Also, every
code base needs a certain amount of refactoring and maintenance work to remain in a clean state (or
to
improve). Hence, we want developers motivated and eager to change the code, but the processes
incentivize them not to due to the complexity and work they add. This is especially problematic if
all work needs to be planned (e.g. in a Scrum sprint planning) and this planning only occurs in
certain time intervals. Slowing developers down like this fossilizes the code base and shifts the
focus from doing the work to managing it. Especially if your code base is in a bad state and if you
have a lot of maintenance work, you want to reduce all the processes slowing your developers down to
a bare minimum. The only way you'll get out of this bad situation is by doing more development work,
i.e. refactoring, writing automated tests and fixing bugs. Doubling down on processes will only
freeze the current state. Most likely, this isn't what you want.

Another bad software development practice is splitting a topic between different development teams.
For example, you might have a front-end team and a back-end team for a time tracking application.
This is a bad idea as it encourages a very limited view on the end-to-end solution. Rather than
feeling responsible for the whole product, the subteams will only care about their own part.
Obviously, this is not ideal. This bad idea becomes even worse if central teams are involved. For
example, let's assume that a central team is responsible for all UI development. The application
team then has to negotiate how the UI is supposed to look with this central team who will then do
the development and hand the finished UI back to the application team for maintenance. There is a
reason advocates of agile software development have strongly recommended feature teams over the last
twenty years: It gives everybody in the team the incentive to take an end-to-end view of the
product.

Next, we have to talk about the incentives of the hiring processes. I'm completely convinced that
it's better not to hire someone than to hire
a [bad developer](https://thinkingsideways.net/people/developer-skill-matrix.html). However, this
philosophy may get sabotaged by the hiring process. If offerings expire or are reviewed again after
a certain time then managers are pushed towards filling the position even if they cannot find a
truly suitable candidate. Hiring budgets vary from quarter to quarter in large companies and
experienced managers know that this places them in danger of losing the open position altogether.
Hence, they will rush to fill the position if the end of the quarter looms ahead. In the long run,
you'll end up with subpar development teams, especially if you're located in a country where you
can't just fire anyone not keeping up. Everything becomes harder if you have a bad development team,
so I cannot stress enough how important it is to only hire good people.

Last, I want to mention that we developers also incentivize the management. The more we appear to
have things under control, the more freedom we have. The more we mess up, the more the managers will
feel the need to intervene. They will want to either help us by adding more people or to control us
via more and more elaborate processes. Let's not give them any reason for this. We can only insist
on empowerment if we deliver high quality, maintainable software and keep our customer's happy. So,
keep the quality high unless you want more complex processes in your life.

That completes our look at incentives. I hope you enjoyed it. If you did, please share it with
somebody. You can also follow me on [Twitter/X](https://twitter.com/fxr256). 