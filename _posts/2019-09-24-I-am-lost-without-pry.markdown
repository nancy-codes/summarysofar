---
layout: post
title:  "I am lost without pry"
date:   2019-09-24 00:18:25 -0600
---
One thing I learned in programming is, when in doubt, just throw pry. Pry is a runtime developer console, an excellent debugging tool, an alternative to IRB. It helps you navigate through the unfamiliar part of your code. For instance, place `binding.pry` somewhere in the middle of a unit test. Depending on whether it is hit or not, you get a hint of where things are broken. If you get into the pry, you can safely assume that anything above that pry has passed successfully. Or when you've just created a new method and are unsure of what to do next, just throw pry and type `self`. And play around with it to figure out the purpose of a given method.

{% highlight ruby linenos %}
def add
  binding.pry
end
{% endhighlight %}

You can have multiple `binding.pry`'s and type `exit` to move onto the next one. Sometimes, even if you have just one pry within a particular function, you may have to exit several times in order to test a specific part or nth iteration of a loop.

Since I rely heavily on pry in testing, I should know better about how it exactly works. I found **[this article](http://kyrylo.hatenablog.com/entry/2013/05/29/so-what-is-binding-pry-exactly)**, written by someone who had the same question and shared an informative post on this important subject.
