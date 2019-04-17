---
layout: post
title:  "Why so Many Developers don't Write Automated Tests"
date:   2019-03-15 17:13:01 +0100
categories: testing
---
How much of your code is covered by automated tests? Chances are, the precentage is not as high as you would like. In my time as a software developer, I have worked in code-bases with a high coverage as well as in onces with barely any tests at all. I vastly prefer the former as a good automated test suite speeds up development and makes it much easier to determine whether the current state of the code is ready for production. The advantages of automated testing is well-known in the industry, but automated testing has never reached the ubiquity one might expect given its advantages. In fact, from my experience, teams with a high degree of automated tests are the exception rather than the norm. In this article, I'll flesh out my explanation for this. From my experience, there are three lacks at the heart of the problem:

#### Lack of knowledge
It is hard to do something properly if you don't know how. Many developers have only a superficial understanding of how to write automated tests. They may have visited a training a few years ago, but lack the necessary pratical experience. Or they may have to deal with an outdated and badly kept code base which makes testing quite difficult. Adding tests to legacy code is quite difficult and requires specific knowledge. Without it, the task may be daunting and this in turn will prevent developers from even attempting it. 

#### Lack of Time
The most obivious lack of all. Time is always an issue in software development. No matter how careful the planning is, how slim the processes are and how good the code quality is, there always seems to be too little time to do things perfectly. Writing automated tests takes time at first even though it pays back in the mid-term. However, the developers need to have the necessary space to make the initial investment. If you currently have little to no automated test coverage, you might need to reserve some time to get the ball rolling.

#### Lack of Interest
The most troubling lack.