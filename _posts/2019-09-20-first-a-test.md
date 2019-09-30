---
layout: post
title: First, a test
date: 2019-09-20 17:37 -0600
---
The first principle that I was told regarding software development was this: 'Always, always, always, write tests first'. In short, 'AAA WTF'!

In technical terms, this principle is called "Test Driven Development" (TDD). It means that before implementing a feature, you need to write a test for that feature.

Before I lose you, let's start with something concrete. Since I'm hungry, let's make some bread.

```
$ mkdir test
$ atom test/bread_test.rb
```

If you `atom` something on the command line, it will create and open a new file at the same time. Since we're testing for the Bread class, we name the test that reflects our intention. That is, we append `_test` to the file name.


{% highlight ruby linenos %}
# ./test/bread_test.rb

require 'minitest/autorun'
require 'minitest/pride'
require './lib/bread'

class BreadTest < Minitest::Test

end
{% endhighlight %}

Inside the test file, we need to have some gems and dependency files to begin with. MiniTest is a popular tool for automated unit testing framework. Our BreadTest class will inherit from `Minitest::Test`. What does that `::` mean? That means our Bread class will inherit some very nice assertion methods from `Test` module within MiniTest.

`minitest/autorun` allows us to run all our tests easily; `minitest/pride` adds coloring to our test output -- without this gem, I wouldn't be able to see those bright green dots.


In general, a test would include 3 parts: `setup`, `execution`, and `assertion`. Below is a code snippet that illustrates the basic structure of a test.

{% highlight ruby linenos %}
def test_it_exists
  pain_au_chocolat = Bread.new("Pain au chocolat", 3)

  assert_instance_of Bread, pain_au_chocolat
end

def test_attributes
  pain_au_chocolat = Bread.new("Pain au chocolat", 3)

  assert_equal "Pain au chocolat", pain_au_chocolat.name
  assert_equal 3, pain_au_chocolat.price
end
{% endhighlight %}

Here, we have two unit tests for the Bread class (which still hasn't been created yet). We test its very existence and its attributes, if there's any. As you may have noticed, all test names must be prefixed with `test_`. There is a nice keyboard shortcut that returns a basic test. Just type in `def`, followed by `t`, and hit the tab key.

Now, we are testing for existence and attributes. First, setup: make a new instance of Bread class, initializing it with two parameters (aka, the name of the bread and its price). In this basic test, we don't have any method to execute, other than the instance's attributes. So we move on to the assertion part.

The assertion part compares two values: expected and actual. For existence, we assert that `pain au chocolat` is an instance of Bread class. For attributes, we check if the expected values match the attributes of the instance.   

Finally, time to create the Bread class, so we can make our tests pass.


```
$ mkdir lib
$ atom lib/bread.rb
```

{% highlight ruby linenos %}
# lib/bread.rb
class Bread

  attr_reader :name, price

  def initialize(name, price)
    @name = name
    @price = price
  end
end
{% endhighlight %}

There is a lot going on here. First, let's start with initialization. When we are instantiating a Bread class (in other words, make a new instance of this class), we require two parameters (i.e., `name` and `price` attributes), without which the new instance won't be created.

Then we can prepend an @ sign to these attributes to make them "instance" variables. By doing so, we don't limit them only inside the `initialize` method. We can call them in other methods within the Bread class. Furthermore, we can make them available as methods (which are public by default in Ruby), by adding them to `attr_reader` method. Now, we can call `name` and `price` methods directly on any Bread instance.

The tests are now passing. Now I get to grab some pain au chocolat!
