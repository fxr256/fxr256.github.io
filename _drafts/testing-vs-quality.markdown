---
layout: post
title:  "Testing vs Quality"
date:   2019-05-03 17:13:01 +0100
categories: testing
---
Testing and quality. For a lot of people, these two words are so closely linked that it is tough to tell them apart. They think that the solution for bad software quality is to test more. The truth is very different. Let me make it as clear as possible:
>Testing does not raise quality!
I expect that a lot of readers will challenge this statement. This is quite understandable, as testing and quality are related, but the relationship is much looser. Testing can show you the **absence** of quality, by exposing the bugs in your software to the light of day. However, it can only proof the presence of bugs and not the inverse: Just because you didn't find any bugs, doesn't mean that there aren't any left in the code. So, testing is a quality check and not even a very reliable one. Nevertheless, testing has an impact on quality if you find bugs and decide to fix them. Afterwards, your code hopefully will be in a better state than before. This is why so many people directly link testing and quality, but this is an oversimplification. Just as you don't fill up your gas tank, just be checking how much is left, you don't raise your software quality just be testing it. Instead, you have to take action and explicitly improve the software quality.

To cover:
	Tests don't raise quality
	Tests can only proof the existence of bugs, not their absence
	No "fig-leave" testing
	You need to adress the findings
	If you have poor quality, testing is not the answer
	Manual testing is a poor investment
	Guided manual testing is dehumanizing and pointless