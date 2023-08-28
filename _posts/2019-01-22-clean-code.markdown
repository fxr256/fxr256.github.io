---
layout: post
title:  "Clean Code in Real Life"
description: "This blog post contains multiple examples of real life code and describes how you can transform the ugly code into clean code."
date:   2019-01-22 18:00:01 +0100
categories: code
redirect_from: clean/code/2019/01/22/clean-code
---
Let's talk about clean code. You've probably heard about it at some point during the last years and most software engineers will agree that clean code is important. But what exactly is clean code? Michael Feathers defines it as follows:
> Clean Code always looks like it was written by someone who cares.

What does this mean? In a nutshell, clean code boils down to the following five rules:
1. Use proper names
2. Keep methods short
3. Keep classes short
4. Don't repeat yourself
5. Keep your code free of side-effects

I want to keep the discussion of these rules short. For a more detailed introduction, you can either read [this article](https://hackernoon.com/let-the-code-speak-52d1cebf0394) or read the [book](https://www.goodreads.com/book/show/3735293-clean-code) which started it all. Let's only briefly talk about naming and method / class length. 

Naming is one of the hardest things in software development. Many programmers dislike longish names, mostly because they take so long to type. To produce clean code, you have to get over this. Code is much more often read than written and short names often make the code hard to understand. Abbreviations require mental mapping which is unnecessary and will confuse new team members. For example, `context` is a much better name than `ctx` and `timeAccount` should be preferred over `ta`. A variable should contain exactly what it says on the box. You may need several attempts to come up with a good name. This is perfectly normal and a good IDE will make renaming easy in case you come up with a better name at a later point in time.

Proper naming is not only important for variables, but also for methods and classes. For methods, you should make sure that the signature and return type match the method name. For example, a method starting with `get` and a `void` return type is confusing. The same is true for methods with a `boolean` return type which only return `true` or throw an exception. For classes, stay away from generic names like `manager` or `helper`. Try to make the purpose of the class as clear as possible. Rename the class if its name does not fit its purpose anymore. If you limit the size of your classes, finding a good name is 
easier (see next paragraph).

What does it mean to keep your classes and methods short? Obviously, the concrete number of lines varies depending on your programming language. For class length, I like to follow Robert C. Martin's advice that a class should only do one thing. This usually limits you to at most 200 lines in Java. A good indicator for a too big class is that you feel tempted to write unit tests which directly call private methods. This means that there is another class hidden in your class which wants to get out. For method length I try to limit myself to at most 20 lines in Java. This may seem absurdly short for you, but it is important to understand that methods are not only useful for code reuse but also for improved readability. In a lengthy method you usually have several blocks of related code. For example, you might read some code from the database, then do some calculations on it and then format it to a suitable format for the UI. Each of these code blocks should be in a dedicated private method. So, you would end up with a `getDataFromDatabase` method, a `calculate` method and a `getUIData` method. Your formerly lengthy method then only contains calls to these private methods rather than a lot of unstructured code. This greatly improves readability as it allows you to understand a method's structure and purpose on a higher level of abstraction. This idea is brought to its logical conclusion in the [single level of abstraction principle](http://www.principles-wiki.net/principles:single_level_of_abstraction). 

With this out of the way, let's head over to code. All of the following code samples are derived from the codebase of a huge commercial enterprise Java project. I have changed them to protect the innocent while trying to keep the original problems in place.

{% highlight java %}
public class ShopCreationResult extends CreationResult {

private List<ShopResultBean> shops = new ArrayList<>();

public List<ShopResultBean> getShops() { 
	return shops; 
}
{% endhighlight %}

So, what's wrong with this code? This class is simply a container for the result of an operation. It is more similar to a `struct` in C than to a proper object. While this is troubling from an object-oriented point of view, it is quite common in Java. The core problem here is improper naming. The variable `shops` is wrongly named. It does **not** contain shops, but the result of a shop creation. There is a mismatch between the type and the name of the variable. Shortening the name like this is misleading, similar to calling a banana split a banana. Also, the type `ShopResultBean` is not properly named as well. Fortunately, all this is easy to fix:

{% highlight java %}
public class ShopCreationResult extends CreationResult {

private List<ShopCreationResultBean> shopCreationResultBeans = new ArrayList<>();

public List<ShopCreationResultBean> getShopCreationResultBeans() { 
	return shopCreationResultBeans; 
}
{% endhighlight %}

There, much better. Now, type and variable name are aligned. One might argue that the names are too long now, but in my opinion this isn't a problem: Clarity is more important than compactness. Using the type name as a variable name causes some redundancy, but is unavoidable in a strongly typed language as Java. Remember that the type is only clearly visible at the declaration while the variable name can be used throughout the whole codebase. Let's look at the next example:

{% highlight java %}
public class MissingShopCreator {

public ShopCreationResult execute(ShopType shopType, Location location, boolean batchMode) {
// method content omitted for compactness
}

private void markObsoleteShopForDeletion(shopId) {
// method content omitted for compactness
}

// a dozen other private methods omitted for compactness
{% endhighlight %}
This is a more complicated case. We have a class with just one public method called `execute` and a lot of private methods used to structure the code. As this class is called `MissingShopCreator` we can safely assume that its purpose is to create things. However, looking more closely at the private methods, we find a method called `markObsoleteShopForDeletion`. So, this class does not only create things, sometimes it also flags things as obsolete as well. This is very confusing for both users of this class as well as code maintainers. Nobody would expect the logic marking shops for deletion in a class named `MissingShopCreator`. The code only got in this state because `MissingShopCreator` was extended with more and more features as the time went on. It was a short and properly named class once, but over the years it put on a lot of fat and the name became confusing.

So what to do? A small improvement would be to change the name. However, you would probably end up with something exceedingly abstract and generic like `ShopManager`. The better fix is to properly refactor the class and split it up into smaller, more concise and properly named pieces. This should have happened at some point in the past when the class was modified, but there are always a lot of good reasons not to improve the existing code. This example shows that it is critically important to revisit your code whenever you make a change. Otherwise, your once beautiful code can turn ugly very fast. [Continous Design](https://msdn.microsoft.com/en-us/magazine/ee294453.aspx) is the only way to ensure that your code will not deteriorate over time.

Another thing we need to pay attention to are comments. Some people believe that comments are essential for readable code. I strongly disagree. Clean code does **not** require any comments to be readable. Whenever you feel the need to comment your code think about changing the code itself instead. Comments can be misleading and outdated while the code always tells the truth. If you don't pay close attention to your comments, you can end up with code like this:

{% highlight java %}
// special treatment for leave of absence.
if (!isLoA) {
  endDate = this.getEndDateForNonLoA();
} else {
  endDate = this.getExpectedReturnDate();
}
{% endhighlight %}
This code snippet deals with employee absences. The comment at the top of the if-statement is out of place as it clashes with the checked condition. Maybe the author intended to mark the whole if-block with the comment or maybe it was appropriate at one point in time, but now it only causes confusion. Fortunately, the fix is easy: Just delete the comment; it is pointless anyway.
You should only add a comment to tell the reader something which **cannot** be learned from the code. One example for this could be a comment telling the reader why the problem is solved in a certain way. There might have been alternative solutions which were already tried and discarded. Such a comment might be helpful as it prevents repeating past mistakes.
While we are on the subject of comments: Commented out code is waste, clutters the code base and causes confusion. Hence, it needs to be deleted without mercy. Current version control systems are powerful enough that you will always be able to restore the code if you need it. 

There is one last example which I would like to present:
{% highlight java %}
private boolean compareBalanace(BigDecimal oldBalance, BigDecimal newBalance ){
  if(oldBalance != null && newBalance != null){
    if (oldBalance.compareTo(newBalance) == 0){
      return true;
    }
  } else {
      return Objects.equals(oldBalance, newBalance);
  }
  return false; 
}
{% endhighlight %}
What can be improved here? The most obvious problem is the spelling mistake in the method name. But let's look at the method name in general. What does `compareBalance` actually mean? This method returns a boolean, so the method will probably be used in some kind of if-statement. `CompareBalance` does not tell you what actually is getting compared and when the method will return `true`. Also, the name implies an integer return type in Java conventions.
The usage of `compareTo` in the method body might raise some eyebrows, as it is only used to check for equality. There is a reason for this which might be made clearer with a comment. Here is an improved version of the code:
{% highlight java %}
private boolean isBalanceUnchanged(BigDecimal oldBalance, BigDecimal newBalance ) {
  if (oldBalance != null && newBalance != null) {
    // uses "compareTo" rather than "equals" to ignore trailing zeros during the comparison (we want "0.0" to be equal to "0")
    if (oldBalance.compareTo(newBalance) == 0) {
      return true;
    }
  } else {
      return Objects.equals(oldBalance, newBalance);
  }
  return false; 
}
{% endhighlight %}

It is important to remember that writing clean code is an iterative process. Newly written code is usually ugly. You clean it up after it runs by slowly refining it until you are satisfied with it. The same is true for existing code. Whenever you touch "old" code, you should strive to leave it in a better state afterwards. If you keep doing that, your codebase will become more and more clean over time. I hope these examples were helpful to you. If you liked this blog post, please share it with somebody. You can also follow me on [Twitter/X](https://twitter.com/fxr256).