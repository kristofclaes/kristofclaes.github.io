---
title: Don't dehydrate your code
---

DRY is one of the most overused principles in software development and the world would be a better place if a lot of code was a bit more MOIST. (I'm still looking for a relevant catch phrase that has MOIST as an acronym.) There, I've said it. Before you close your browser, allow me to explain myself.

## A lack of pragmatism

Where everyone agrees that principles should be applied pragmatically, it appears that DRY is exempt from any form of pragmatism. When I read blog posts, questions and answers on StackOverflow, or talk to people, I often have the impression that all code should be as DRY as possible at all times. I have often seen this lead to unnecessary (and overly complex) abstractions that only exist for the sake of DRYing up code. As we all know, naming things is jokingly said to be one of the hardest things in software development. Unnecessary and complex abstractions combined with bad naming gives you code that is hard to read and hard to maintain. DRY should lead to code that is easy to understand and maintain, but a lot of times the exact opposite is achieved.

## It's all about context

I'm all for avoiding repetition, but not all code that looks similar serves the same purpose. You should keep the context of the code in mind when trying to determine if two instances of seemingly similar code are actual repetitions or not.

Let's look at these two classes:

{% highlight python %}
class Book(object):
    def __init__(self):
        self.pages = []

    def add_page(self, page):
        if len(self.pages) > 1000:
            raise Exception('Max 1000 allowed.')

        self.pages.append(page)


class Box(object):
    def __init__(self):
        self.items = []

    def add_item(self, item):
        if len(self.items) > 1000:
            raise Exception('Max 1000 allowed')

        self.items.append(items)
{% endhighlight %}

The `add_page` and `add_item` sure look similar. A lot of people might argue some refactoring is needed to DRY things up. They might end up with something like this:

{% highlight python %}
class ContainerBase(object):
    @staticmethod
    def add_to_list(item, item_list):
        if len(item_list) > 1000:
            raise Exception('Max 1000 allowed.')

        item_list.append(item)


class Book(ContainerBase):
    def __init__(self):
        self.pages = []

    def add_page(self, page):
        self.add_to_list(page, self.pages)


class Box(ContainerBase):
    def __init__(self):
        self.items = []

    def add_item(self, item):
        self.add_to_list(item, items)
{% endhighlight %}

Look at this lovely DRY code! But then the requirements change. You need different exception messages for books and boxes. Because of thinner paper, you can now have books with 1500 pages. Specific types of items can only appear twice in a box.

Before you know it the `add_to_list` methods takes 6 parameters, including three booleans to toggle behavior. But hey, the code is DRY.

Books and boxes have nothing in common. They don't share any business rule. The initial rules "Books can't contain more than 1000 pages" and "Boxes can't contain more than 1000 items" are exactly that: two separate rules. They may look similar, but they are two different rules nevertheless and shouldn't be represented as one in the code.

## My advice

Don't prematurely DRY up your code. We've all learned we shouldn't prematurely optimize our code. It's time we treat DRY the same. It's OK to have similar or identical code in two or more different places. There's absolutely nothing wrong with that.

It _can_ become a problem when you have to make changes to such pieces of code, but as long as you don't, there's no problem at all.

Let's go back to our previous example of books and boxes. Suppose a feature request comes in asking to allow books to have up to 1500 pages. With the `ContainerBase` you have two options:

1. You forget (or don't know) the `ContainerBase` is used by `Box` as well. You now have introduced boxes that can hold up to 1500 items. Congratulations on your new bug!
2. You remember the `ContainerBase` is used by `Box` as well and take it into account. Everything is OK, but you had to do some unnecessary work. Combine that with the amount of time you spent prematurely DRYing up the code. Now look at your velocity and cry as you realize how much business value you could have added instead.

Without the `ContainerBase` class, you would only need to change one simple thing in the `Book` class. But let's say that after the release of the feature request you receive an email saying that they actually also wanted boxes to be able to hold 1500 items. No problem, just another simple change to the `Box` class. But at this point, you should make a note that `Book` and `Box` were changed at the same time in a similar way. If this becomes a trend for these two classes, it's time to refactor them and extract shared logic.

I really don't see the advantage of prematurely DRYing up your code. There's always the chance you were right and made the right decision of course, but a lot of times you just don't know how things will have to behave or change in the future. Especially if you're taking an agile approach and build and release features iteratively, you just can't be sure. It's more time consuming to fix incorrect DRYness than it is to retroactively make a correct decision and make things more DRY. That's time that could be spent delivering business value or writing unit tests instead.

In the end, it all comes down to this: YAGNI > DRY.
