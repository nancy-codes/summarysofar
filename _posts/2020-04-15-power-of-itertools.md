---
layout: post
title: Power of itertools
date: 2020-04-15 18:26 +0900
---
No need to look further when you're trying to dig deeper into something. Reviewing the basics can be (or should be) repeated. So, among 69 Python [built-in functions](https://docs.python.org/3/library/functions.html#built-in-funcs), I will focus on 4 of them associated with looping. Namely, `range`, `map`, `filter`, and `zip`. To make this review process more engaging, I have assumed the role of a translator sitting between a human and a computer.

<center><img width="70%" alt="builtins" src="https://user-images.githubusercontent.com/24424825/79321675-ac195100-7f46-11ea-884a-0e31bc423127.png"></center>
<br><br>

#### Range
<br>
:raising_hand: **Write down ten multiples of 7, starting from 7.**

```
list(range(7, 70, 7))
>> [7, 14, 21, 28, 35, 42, 49, 56, 63]
```

Here, `range` function accepts 3 parameters, `start`, `stop`, and `step`. Start is inclusive, Stop is exclusive. The function returns an iterator object. To output the actual value, the object needs to be wrapped in a list.

<br>

#### Map
<br>
:raising_hand: **The previous example can be generalized to include multiples from 2 to 9, simulating a multiplication table.**

> Let's say your little cousin is studying the multiples of 6.

```
for i in map(lambda x, y: (x, y, x*y), repeat(6), range(10)):
		print('{:d} * {:d} = {:d}'.format(*i))

6 * 0 = 0
6 * 1 = 6
6 * 2 = 12
6 * 3 = 18
6 * 4 = 24
6 * 5 = 30
6 * 6 = 36
6 * 7 = 42
6 * 8 = 48
6 * 9 = 54
```

Here, `map` function accepts three parameters: a lambda function as an object, followed by two iterables: repeat 6 for x value, and a sequence from 0 to 9 for y value. The placeholder `d` is used for `signed integer decimal`, since we're dealing with integers.

<br>

#### Filter
<br>
:raising_hand: **Imagine a dictionary of people and the number of `___`, you fill in the blank. You want to only "filter" people with the item.**

```
people = {'Mary': 2, 'Pete': 1, 'Frank': 0, 'Julie': 0}
```

A filter function returns a boolean value. It will evaluate the input (the value of each person) and return True if it's greater than 0, and False if it's 0.

```
def has_something(pair):
		return bool(pair[1])
```

The following loop will return those who meet the condition, specified by the `has_something` function.

```
for person, something in filter(has_something, people.items()):
		print(person)

>>
Mary
Pete
```

Note that the iterable is `people.items()`, not just the dictionary `people` in order to access both key and value.

<br>

#### Zip
<br>
:raising_hand: I'd like to make sure that you eat a different fruit for each day.

`zip()` function consumes an iterable and outputs an iterator in Python 3. It can consume more than one iterable. There are a few use cases for this zip function, but let's play around with a fruity example first.

```
fruits = ['apple', 'orange', 'banana', 'strawberry', 'cherry']
days = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday']

for d, f, in zip(days, fruits):
		print(f'{d}: {f}')

Monday: apple
Tuesday: orange
Wednesday: banana
Thursday: strawberry
Friday: cherry
```

Or we can go from backwards too. If we start with a list of tuples like this:

```
weekly_fruits = [('Monday', 'apple'),
 ('Tuesday', 'orange'),
 ('Wednesday', 'banana'),
 ('Thursday', 'strawberry'),
 ('Friday', 'cherry')]
```

And you'd like to separate each pair into independent lists, then you can unzip it with the unpacking operator `*`.

```
days, fruits = zip(*weekly_fruits)

days
>> ('Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday')
fruits
>> ('apple', 'orange', 'banana', 'strawberry', 'cherry')
```



Another use case for `zip` function is constructing a dictionary. Let's say keys and values are given as separate lists.

```
keys = ['name', 'dob', 'likes', 'dislikes', 'quotes']
values = ['Sonia', '1995-03-03', 'Coffee', 'Cauliflower', 'No need to look further']
```

Then you can zip with and wrap it with a dictionary.

```
user_dict = dict(zip(keys, values))

user_dict
>> {'name': 'Sonia',
 'dob': '1995-03-03',
 'likes': 'Coffee',
 'dislikes': 'Cauliflower',
 'quotes': 'No need to look further'}
```

Granted this approach isn't aligned with OOP, but at least the `keys` list is reusable and you can zip it with a new user value quickly!

<br>
#### References

- [Itertools 1](https://pymotw.com/3/itertools/index.html)
- [Itertools 2](https://realpython.com/python-itertools/)
- [zip()](https://realpython.com/python-zip-function/#traversing-lists-in-parallel)
