---
title: Mocking properties in Python
description: How to mock properties in Python using PropertyMock.
---

It doesn't happen all *that* often, but sometimes when writing unit tests you want to mock a property and specify a return value. The `mock` library provides a `PropertyMock` for that, but using it probably doesn't work the way you would initially think it would.

I had this exact problem earlier this week and had to explain it to two different people in the two days after that. So why not write it down in a blog post?

Suppose you have this silly implementation of a class that takes a file path and reads the file's content into a variable that can be accessed through a property:

{% highlight python %}
class SillyFileReader(object):
    def __init__(self, file_path):
        self._file_path = file_path
        self._content = self._read_file()
        
    def _read_file(self):
        with open(self._file_path, 'r') as f:
            return f.read()
        
    @property
    def content(self):
        return self._content
{% endhighlight %}
            
You also have this equally silly function that takes an instance of the silly file reader and returns the reversed content:

{% highlight python %}
def silly_reverse_content(silly_file_reader):
    return silly_file_reader.content[::-1]
{% endhighlight %}
        
Of course you want to test this silly function. Maybe you come up with something like this:

{% highlight python %}
import mock
import unittest


class SillyTest(unittest.TestCase):
    def test_silly_reversing(self):
        mock_reader = mock.MagicMock()
        mock_reader.content = mock.PropertyMock(return_value='silly')

        assert silly_reverse_content(mock_reader) == 'yllis'
{% endhighlight %}
            
Unfortunately, that won't work:

{% highlight plaintext %}
TypeError: 'PropertyMock' object has no attribute '__getitem__'
{% endhighlight %}
    
The thing with a `PropertyMock` is that you need to set it for the type of an object, not for the object itself. To get things working, you need to do it like this:

{% highlight python %}
class SillyTest(unittest.TestCase):
    def test_silly_reversing(self):
        mock_reader = mock.MagicMock()
        type(mock_reader).content = mock.PropertyMock(return_value='silly')

        assert silly_reverse_content(mock_reader) == 'yllis'
{% endhighlight %}
            
That's it!