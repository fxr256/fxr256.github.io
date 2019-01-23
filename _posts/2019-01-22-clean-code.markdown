---
layout: post
title:  "Clean Code in Real Life"
date:   2019-01-22 18:00:01 +0100
categories: clean code
---
Let's talk about clean code. You've probably heard about it at some point during the last years and most software engineers will agree that clean code is important. But what exactly is clean code? Michael Feathers defines it as follows:
> Clean Code always looks like it was written by someone who cares.

What does this mean? In a nutshell, clean code boils down to the follow five rules:
1. Use proper names
2. Keep methods short
3. Keep classes short
4. Don't repeat yourself
5. Keep your code free of side-effects

I'm not going to explain these rules in detail. Instead, I will show you some real-life code samples which violate a few of these rules and how to improve them. If you want a more detailed introdcution, you can either check [this article](https://hackernoon.com/let-the-code-speak-52d1cebf0394) or read the [book](https://www.goodreads.com/book/show/3735293-clean-code) which started all of this. 

With this out of the way, let's head over to code. All of the following code samples are derived from the codebase of a huge commercial project. I have changed them to protect the innocent while trying to keep the original problem in place.

{% highlight java %}
public class ShopCreationResult extends CreationResult {

private List<ShopResultBean> shops = new ArrayList<>();

public List<ShopResultBean> getShops() { 
	return shops; 
}
{% endhighlight %}

So, what's wrong with this code? This class is simply a container for the result of an operation. It is more similar to a struct in C than to a proper object. While this is troubling from an object-oriented point of view, it is quite common in Java. The core problem here is naming. The variable `shops` is wrongly named. It does NOT contain any shops, but the result of a shop creation. There is a mismatch between the type and the name of the variable. Shortening the name like this is misleading, similar to calling a banana split a banana. Also, the type `ShopResultBean` is not properly named as well. Fortunately, all this is easy to fix:

{% highlight java %}
public class ShopCreationResult extends CreationResult {

private List<ShopCreationResultBean> shopCreationResultBeans = new ArrayList<>();

public List<ShopCreationResultBean> getShopCreationResultBeans() { 
	return shopCreationResultBeans; 
}
{% endhighlight %}

There, much better. Now, type and variable name are aligned. One might argue that the names are too long now, but in my opinion this isn't a problem. Long names are only annoying when writing code. As code is much more often read than written, clarity is more important than compactness. Using the typename as a variable name causes some redundancy, but is unavoidable in a strongly typed language as Java. Remember that the type is only clearly visible at the declaration while the variable name can be used throughout the whole codebase. Let's look at the next example:

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
This is a more complicated case. We have a class with just one public method called `execute` and a lot of private methods used to structure the code. As this class is called `MissingShopCreator` we can savely assume that it's purpose is to create things. However, looking more closely at the private methods, we find a method called `markObsoleteShopForDeletion`. So, this class does not only create things, sometimes it also flags things as obsolete as well. This is very confusing for both users of this class as well as any code maintainers. Nobody would expect the logic marking shops for deletion in a class names `MissingShopCreator`. The code only got in this state because `MissingShopCreator` was extended with more and more features as the time went on. It was a short and properly named class once, but over the years it put on a lot of fat and the name became confusing.

So what to do? A small improvement would be to change the name. However, you would probably end up with something exceedingly abstract and generic like `ShopManager`. The better fix is to properly refactor the class and split it up into smaller, more concise and properly named pieces. This should have happend at some point in the past when the class was modified, but there are always a lot of good reasons not to improve the existing code. This example shows that it is critically important to revisit your code whenever you make a change. Otherwise, your once beautiful code can turn ugly very fast. [Continous Design](https://msdn.microsoft.com/en-us/magazine/ee294453.aspx) is the only way to ensure that your code will not deteriorate over time.

Another thing we need to pay attention to are comments. Some people believe that comments are essential for readable code. I strongly disagree. Clean code does **not** require any comments to be readable. Whenever you feel the need to comment your code think about changing the code itself instead. Comments can be misleading and outdated while the code always tells the truth. If you don't pay close attention to your comments, you can end up with code like this:

{% highlight java %}
// special treatment for leave of absence.
if (!isLoA) {
  endDate = this.getEndDateForNonLoA();
} else {
  endDate = this.getExpectedReturnDate();
}
{% endhighlight %}
This code snippet deals with employee absences. The comment at the top of the if-statement is out of place as it clashes with the checked condition. Maybe the author intended to mark the whole if-block with the comment or maybe it was appropriate at one point in time, but now it only causes confusion. Fortunately, the fix is easy: Just delete the comment. While we are at it: Commented out code is an abomination and needs to be deleted without mercy. It clutters the code base and causes confusion. Just delete it. Current version control systems are powerful enough that you will always be able to restore the code if you need it. You should only add a comment to tell the reader something which **cannot** be learned from the code. One example for this could be a comment telling the reader why the problem solved in a certain way. There might have been alternative solutions which were already tried and discarded. Such a comment might be helpful as it prevents repeating past mistakes.

There is one last example which I would like to present:
{% highlight java %}
  private boolean compareBalanace(BigDecimal oldBalance, BigDecimal newBalance ){
      if(oldBalance != null && newBalance != null){
        if (oldBalance.compareTo(newBalance) == 0){
            return true;
        }
      } else {
           return Objects.equals(oldBalance,newBalance);
      }
    return false; 
  }
{% endhighlight %}
What can be improved here? The most obvious example is the spelling mistake in the method name. But let's look at the method name in general. What does `compareBalance` actually mean? This method returns a boolean, so the method will probably be used in some kind of if-statement. `CompareBalance` does not tell you what actually is getting compared and when the method will return `true`. Also, the usage of `compareTo` here might raise some eyebrows, as it is only used to check for equality. There is a reason for this which might be made more clear with a comment. Here is an improved version of the code:
{% highlight java %}
  private boolean isBalanceUnchanged(BigDecimal oldBalance, BigDecimal newBalance ){
      if(oldBalance != null && newBalance != null){
      	// uses "compareTo" rather than "equals" to ignore trailing commas during the comparison
        if (oldBalance.compareTo(newBalance) == 0){
            return true;
        }
      } else {
           return Objects.equals(oldBalance,newBalance);
      }
    return false; 
  }
{% endhighlight %}

Much better. It is important to remember that writing clean code is an iterative process. When you write new code, it is usually ugly. You clean it up after it runs and works by slowly refining it until you are satisfied with it. The same is true for existing code. Whenever you touch "old" code, you should strive to leave it in a better state afterwards. If you keep doing that, your codebase will become more and more clean over time. I hope these examples were helpful to you.