---
layout: post
title:  "Beyond Email: Leveraging Issue Trackers for Effective Communication"
description: "Issue trackers offer many advantages over more traditional communication channels like email and should be used primarily."
date:   2023-05-26 08:26:01 +0100
categories: processes
---
Today I want to talk about [issue trackers](https://en.wikipedia.org/wiki/Issue_tracking_system). These systems help keep track of work items like support requests, open bugs and feature requests. They come in different shapes for different purposes: some, like [ServiceNow](https://www.servicenow.com/), focus on support requests, some, like [Bugzilla](https://www.bugzilla.org/), primarily deal with bugs, while others, like [Jira](https://www.atlassian.com/software/jira), try to capture more or less everything. These systems are very popular (at least with managers, end-users [don't always feel the same way](https://ifuckinghatejira.com)), but I still think that they are underused as a communication channel. Hence, I want to explain why you should use your issue tracker as your primary communication channel. Note, that "primary" *doesn't* mean that **all** communication should take place in the issue tracker. There will be situations where a different medium like chat, a phone call or a face-to-face meeting will be more appropriate. That said, I still think that it is beneficial to use your issue tracker for the majority of your communication. Here are my reasons:

#### Improved Knowledge Sharing
In contrast to email, issues trackers are public. As a result, everyone who is interested in a certain topic can  get up to date information. This is very helpful in big software projects where it is unlikely that you know who's working on what. If you encounter a bug, you can just search for this problem in your issue tracker and hopefully you'll find that someone has already reported the issue. You can then watch the issue for updates. If there is no issue yet, you can just create one which will serve as the central knowledge sharing hub for this topic in the future. This is a great way to share information with the rest of the organization including progress updates. Managers and project managers should be able to tell how well the project is going by just looking at the issue tracker which makes it unnecessary to ask developers for process reports.

#### Improved Collaboration
Issue trackers provide visibility about who is working on what and with what priority. This can improve collaboration as team members can comment, ask questions, and share relevant information directly within the issue. 

#### Improved Communication Structure 
Unlike traditional communication methods, issue tracking systems provide a structured format for communication. Each issue is assigned a title, a description, as well as other relevant details, making it easier for team members to understand the context and requirements. This clarity reduces miscommunication and facilitates keeping everyone on the same page.

#### Traceability and Documentation
Issue tracking systems maintain a comprehensive history of all activities related to tasks, including comments, changes, and updates. This traceability is valuable for tracking decisions and understanding the evolution of a task.

#### Providing Context for Code Changes
Sometimes you discover a bug which was introduced by an old code change and have no idea why the code was changed in the first place. This can be a problem as you don't know whether you will break some functionality or reintroduce an old bug when you fix the current issue. Issue trackers can provide the necessary context here as long as developers always include the issue id in their commit messages. With this information, you can find the original issue which should tell you why this code change was made and what to consider when you fix the current bug.

#### Scalability
Issue trackers can handle projects of every size because you can control how much information is pushed to you and pull whatever information you need when you need it. This is a big advantage over email and chat as people tend to get overwhelmed when they receive too many mails or chat messages and have no easy way to reduce that volume.

#### Mandated usage
In many organizations you have to use an issue tracker. If that is the case, it makes a lot of sense to use it as your primary way to communicate. After all, using the issue tracker in a half-hearted fashion and relying on other communication channels like email only increases the communication overhead and makes things more confusing.

### Conclusion
As you can see, there are a lot of reasons why your issue tracker should be your primary communication tool. However, you can only enjoy these benefits if team members use the tracker in a productive way: Issues should describe clearly what they are about including the context, comments should be as clear as possible and all issues should be in the correct state. Without diligent usage of the issue tracker, people will fall back to email as the default communication method even though it is inferior. 

If you liked this blog post, please share it with somebody.