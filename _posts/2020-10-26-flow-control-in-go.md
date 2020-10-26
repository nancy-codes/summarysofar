---
layout: post
title: Flow control in Go
date: 2020-10-26 23:38 +0900
---
Let's talk about loop syntax in Go. 

Examine the syntax below:

```go
days := []string{"Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"}
for i, day := range days {
  fmt.Println(i, day)
}
```

We declare and initialize the `days` variables with a slice of strings, containing 7 days of the week. 

Then from the slice of these strings, we declare and initialize each index and a day variable at every iteration. `range` is a keyword that we use whenever we want to iterate over every single record inside of a slice. In Go's for loop, the braces `{ }` are always required.

Compare this looping construct to that in Ruby and Python.


```ruby
days = ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"]
days.each do |day|
  puts day
end
```


```python
days = ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"]
for day in days:
  print(day)
```

Go has a single looping construct, `for` loop, while the other two languages `while` loops. Go grants a finer control but that comes with more typing. Maybe not so ideal for looping. But Go has strong features including concurrency and memory management, which I will explore in the next step.

