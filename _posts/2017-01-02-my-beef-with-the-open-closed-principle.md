---
title: My beef with the open/closed principle
description: The open/closed principle is too vague and stimulates overly generic code.
---
In a [previous post]({% post_url 2016-12-26-develop-your-poppycock-detector %}) I talked about why it's important to develop a poppycock detector. It can help you to determine when you have to question, investigate or think about things you read or hear. In that post I used this tweet as an example:

>In an ideal system, we incorporate new features by extending the system, not by making modifications to existing code. —Uncle Bob

I tried to explain why it can be dangerous to accept —and repeat— statements like that without giving them further thought. In this post I will go into more detail about *what* it is I don't like about this particular statement.

## The open/closed principe

Let's start with the definition of the open/closed principle:

>In object-oriented programming, the open/closed principle states "software entities (classes, modules, functions, etc.) should be open for extension, but closed for modification"; that is, such an entity can allow its behaviour to be extended without modifying its source code. —[Wikipedia](https://en.wikipedia.org/wiki/Open/closed_principle)

## Why I don't like it

I'm convinced this principle is the cause of a lot overly generic and hard-to-read code covered with layers of indirection. Why? Because a lot of people seem to believe that *all* code should *always* adhere to the open/closed principle. Maybe it's a stage where all developers find themselves in at a specific moment in their career? I know I've been there.

The problem is that developers with an open/closed fixation try to anticipate every possible change or extension to the code. This is bad for a number of reasons.

### It's costly
You spend time (and money) up front for things you may never need. This can be seen as a double loss, because the time you're investing in things you'll never need isn't being spent building things your customers *do* need. Sure, you may save some time later on when it turns out you correctly predicted the future and you do need to implement a change you anticipated, but those occasions are rare.

### You can't predict the future
When writing code it's often pretty easy to come up with ways in which that code or the system will have to be changed in the future. But it's impossible to come up with *every* possible change. Why would you accommodate for possible changes that may never need to happen when you're not doing the same for other changes that may be more likely to be required in the future?

Note that I'm not talking about changes you will need to do in the next sprint or something like that. If you are absolutely sure you need to change or add something, please do design with that in mind.

### Your code becomes overly generic and hard to read
Buy you are a stubborn developer. You take pride in your work, it is your duty to write good code and good code adheres to the holy open/closed principle in every possible way because that's what it says on your t-shirt.

You try to think of all the ways in which the system might need to change in the future and you make sure that those changes will not require any modifications to the code you're writing now. You crown yourself Khaleesi of the Great Generic Sea, Mother of DRYgons and who cares if your code is hard to read? No one will have to change it anyway because you successfully predicted the future!

### You make it hard on your future self
You are very pleased with yourself because you have designed your code in such a way that features Foo and Bar will be super easy to implement. You look at your code and the elegance brings a tear to your eye.

Two years later there's still no need for Foo or Bar, but your customers would be thrilled to get feature Baz. No problem. You dive into the old code thinking it will be a breeze to add Baz. What's this? How does this work? Where is this part implemented? Which idiot designed this code? Time for a git blame! Let's see, ah, here's the commit:

>Add elegant way to extend the system :'-) —You

The code that made your past self almost emotional is making things quite hard for your current self, bringing up feelings from the opposite side of the emotional spectrum. All the work you did to make things extensible turns out to be a bit one-sided. All the useless work you did with extensibility targeted at Foo and Bar in mind is even making it harder than it should be to implement Baz.

## What should you do instead?
The open/closed principle isn't something you should actively work on. It's something you will automatically get a more sensible version of when you write Good Code™. If you follow YAGNI, separate the concerns, separate implementation from intent and write tests from the beginning, your code will automatically become easier to extend. You will have to make modifications to code in the future, but that's not a problem. By following the three simple rules I mentioned you will get code that's easier to maintain and extend without getting in your way than you when you blindly follow and actively pursue the open/closed principle.

For another take on this, I can highly recommend Rob Ashton's excellent blog post [My relationship with SOLID - The big O](http://codeofrob.com/entries/my-relationship-with-solid---the-big-o.html).