---
layout: post
title:  "Abstractions Aren't Free"
description: "This blog post explains why abstractions in software are useful, but have an inheriant cost. Cost and benefit need to be balanced."
date:   2023-07-06 17:26:01 +0100
categories: software design
---
Abstractions are everywhere in software. They make us more productive by allowing us to ignore the small details of the underlying platforms which we are using. For example, we can download something from a server without worrying about the details of [TCP](https://en.wikipedia.org/wiki/Transmission_Control_Protocol), [IP](https://en.wikipedia.org/wiki/Internet_Protocol) or the physical network connections. Also, we can read and write files without having to know how the file system works or how exactly data is stored on a solid-state drive. These abstractions are very useful even though they are [imperfect](https://www.joelonsoftware.com/2002/11/11/the-law-of-leaky-abstractions/). However, abstractions can also be overdone. Overdone abstractions are common in the now more or less obsolete style of elaborate object-oriented programming. This style traumatized a lot of developers during the late 90s and early 2000s and gave birth to concepts like abstract builder factories. Benji Smith wrote a [satire of this programming style](https://web.archive.org/web/20170913103503/http://discuss.joelonsoftware.com/default.asp?joel.3.219431.12) back in 2005 which nicely illustrates the problem. 

There is a lesson to be learned from these historical excesses: Abstractions aren't free and need to provide value. As a general rule we should try to match the level of abstraction we're familiar with. Let's call this our baseline level of abstraction. We are so used to this level of abstraction that we only notice it when it's violated. For example, if we are used to more high-level styles of programming, it would be a violation of our baseline level of abstraction to suddenly have to deal with a block of assembler or having to manually juggle networks packets as these concepts are below our baseline level of abstraction. On the flipside, we also shouldn't introduce higher levels of abstraction than what we're used to. For example, if we usually create new objects directly with a `new` operator, introducing [factories](https://en.wikipedia.org/wiki/Factory_method_pattern) to the code will be jarring. Also, if we usually don't use [object-relational mapping](https://en.wikipedia.org/wiki/Object%E2%80%93relational_mapping) (ORM), then it will be very confusing to suddenly have to use an ORM framework just to make a simple query. Having to use such a framework adds to our mental load as we need to figure out how use it in addition to coming up with the correct query.  

We can also accidently increase the level of abstraction to above our baseline by introducing shared superclasses which represent increasingly abstract ideas. For example, in a human capital management software, there are absences, attendances and work schedules to keep track off. All of these are a combination of an employee and some time information. It might be tempting to create an `EmployeeToTimeInformation` superclass here, but this is a bad idea as the concept is very vague and doesn't match the product domain. Also, there is very little to gain from such an abstraction as the three subclasses are very different in nature. We shouldn't introduce abstractions unless they add significant value as each additional layer of abstraction above our baseline adds more concepts to learn and omits more implementation details which can become very important in certain situations. 

Let's compare two different designs to better understand what too much abstraction looks like. Here is a code snippet on how to write the text "Hello World" to a file called "myFile" in traditional Java:

{% highlight java %}
BufferedWriter writer = new BufferedWriter(new FileWriter("myFile.txt"));
writer.write("Hello World");
writer.close();
{% endhighlight %}
This code is very abstract. We mainly interact with a class named `BufferedWriter` which is a rather vague name and completely unrelated to files. The only hint that we're dealing with a file here is that we pass a `FileWriter` to the `BufferedWriter` as an argument. What do we gain by adding this additional layer of abstraction? Is it even important that we use a buffer here? There are a lot of such abstractions in the Java standard library and I consider most of them pointless. Oracle seems to agree as they have added an alternative way to write to a file in Java 7. It looks like this:
{% highlight java %}
Path path = Paths.get("myFile.txt");
Files.write(path, "Hello World".getBytes());
{% endhighlight %}
This API is far closer to the actual problem we're trying to solve. We can clearly see that we're dealing with files and that we're writing to a file. There are no unnecessary abstractions here.


### Conclusion
Abstractions are useful, but can be overdone. We have a baseline level of abstraction that we're used to and should try to stay on this level. Adding further levels of abstraction should only be done if it adds significant value as learning the new abstract concepts requires effort.

If you liked this blog post, please share it with somebody.


