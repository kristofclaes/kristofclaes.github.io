---
title: Design for readability
description: Code is read much more often than it is written. Design for readability.
---

Surprisingly enough, one of the hardest things to do when you're writing code is to keep things simple. There are many causes why we often make code more complicated than it should be: 

* **Reducing line count.** Even when the "gain" is small we tend to focus on this. It's hard to resist turning three lines of code into one line.
* **Trying to be clever.** Why keep things simple if you can prove you understand lambdas, monads, recursion, reflection and parallelism? Your colleagues will be so impressed!
* **Frameworkitis.** You can't resist the urge to try out the latest JavaScript framework, even though what you're doing is far to simple to justify the use of it.
* **Design pattern hypochondriasis.** An unnecessary concern about missing out on design patterns. You think your code resembles something that's covered by a certain a design pattern and start refactoring your code in order to shoehorn in the pattern.

I try to be conscious of this whenever I'm coding. When you're writing "clever code", the short term high it gives you, makes you forget about the long term consequences. Unnecessarily complex code that you haven't written yourself is hard to grasp. I've often had a feeling that I got the general gist of it, but I felt like I was missing something deeper, on a fundamental level. Why is this code so complex? What am I missing here? I've even had that happen with code I had written myself only months before.

<div class="message">Code is read much more often than it is written. Design for readability.</div>

Try to keep things simple when writing code. That doesn't mean you don't have to think about what you're writing though! Like I said, writing simple code isn't always easier than writing complex code. When you keep things simple it will usually save you time when writing it, but not always. What is almost guaranteed, is that it will save everyone who has to read your code (including the future you!) a lot of time. So even if it would take you longer, it's an investment well worth the effort.