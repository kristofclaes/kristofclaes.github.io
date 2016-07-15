---
title: Code should communicate intent
description: One of the ways to make your code more readable is making sure it is obvious what the code is doing.
---

In a previous post I advocated the principle of [designing for readability]({% post_url 2016-07-02-design-for-readability %}). One of the ways you can achieve a higher degree of readability in your code is making sure it clearly shows what it is supposed to do. If your code communicates intent, it will be much easier for others to grasp the general idea by glancing over it.

## An example please

I have been meaning to write about this for a while, but I couldn't think of a good example. That's one of the problems you face when you want to illustrate something with code. You don't want the example to be overly abstract by limiting it to `Foo`'s and `Bar`'s, but at the same time, you want it to be understandable without having to provide too much context.

When I received a 'Nice answer' badge earlier this week for an answer I posted on Stack Overflow 5 years ago, I stumbled on a great example I wrote myself. What a happy coincidence!

The person asking the question had a simple class that looked like this:

{% highlight csharp %}
public class MyObject
{
    public int ObjectID { get; set; }
    public string Prop1 { get; set; }
}
{% endhighlight %}

The question was how you could remove duplicates from a list of `MyObject` instances. Two instances were considered to be a duplicate of each other if they had the same value for the `ObjectID` property.

The answer that got accepted as the correct one suggested this solution:

{% highlight csharp %}
var distinctList = myList.GroupBy(x => x.ObjectID)
                         .Select(g => g.First())
                         .ToList();
{% endhighlight %}

What this does is it groups the list based on the `ObjectID` and creates a new list with first instance from every group. You probably have to read the entire code block before you realise what it is doing.

My solution was to let the `MyObject` class implement the `IEquatable<T>` interface so you can use LINQ's built-in `Distinct` method.

{% highlight csharp %}
public class MyObject : IEquatable<MyObject>
{
    public int ObjectID { get; set; }
    public string Prop1 { get; set; }

    public bool Equals(MyObject other)
    {
        if (other == null) return false;
        else return this.ObjectID.Equals(other.ObjectID); 
    }

    public override int GetHashCode()
    {
        return this.ObjectID.GetHashCode();
    }
}
{% endhighlight %}

Just by looking at this class you know that the `ObjectID` property defines the identity of the class's instances and that it's used when checking for equality. This can now be used by LINQ's `Distinct`.

{% highlight csharp %}
var myObjects = new List<MyObject>();
myObjects.Add(new MyObject { ObjectID = 1, Prop1 = "Something" });
myObjects.Add(new MyObject { ObjectID = 2, Prop1 = "Another thing" });
myObjects.Add(new MyObject { ObjectID = 3, Prop1 = "Yet another thing" });
myObjects.Add(new MyObject { ObjectID = 1, Prop1 = "Something" });

var distinctObjects = myObjects.Distinct();
{% endhighlight %}

Even though my solution requires more code, I believe it is a lot better because of the intents it communicates:

1. When you look at the class you know how instances will be compared for equality;
2. The use of `Distinct` clearly show that you want to remove duplicates.

## Some pointers

There a quite a few ways you can make the intent of your code more obvious.

### Good naming

Use clear and descriptive names. This counts for everything: classes, variables, properties, methods, functions, ... Don't try to come up with shorter names just to save a few keystrokes. Something like `numberOfAttendees` is longer but far more readable than `attndCnt`. Why do developers seem to have a tendency to leave out vowels? What's up with that?

### Split things up

If it's hard to come up with a clear and descriptive name for a class, a function or a method, that might be a sign that you're trying to do too much in that part of the code. When you split things up it will be easier to name them and if you give them good names people can get away with only reading the names and skipping the implementation.

{% highlight csharp %}
/* Hard to read */
var myString = "The quick brown fox jumps over the lazy dog.";
var vwls = "aeiou";
var tmpList = new List<Char>();
foreach(var c in myString)
{
    if (!vwls.Contains(c))
    {
        tempList.Add(c);
    }
}
var myString2 = new string(tempList.ToArray());

/* Easier to read */
var sentenceWithoutVowels = RemoveVowels("The quick brown fox jumps over the lazy dog.");
{% endhighlight %}

I know there are better ways to remove vowels from a string, but I wanted to show some bad code that's way too long and confusing on purpose. Imagine the better implementation is inside `RemoveVowels`. You don't really need to know *how* it's implemented when glancing over code. You know that that function removes vowels and that's more than enough at that point.

### Use built-in features

If you're trying to do something that's built into the language, framework or library you're using, don't reinvent the wheel. Use built-in features not only for performance reasons, but for recognisability as well. If people reading your code are familiar with the language, framework or library they'll have an easier time understanding your code if they see things they recognise and know.

## Wrapping things up

Making sure your code communicates intent is one of the ways you can design for readability. Naming things is one of the key concepts and it can be surprisingly hard sometimes. Let's end with a famous and relevant computer science joke.

 > There are only two hard things in computer science: naming things, cache invalidation and off-by-one errors.

