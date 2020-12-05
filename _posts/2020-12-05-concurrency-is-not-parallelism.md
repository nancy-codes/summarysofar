---
layout: post
title: Concurrency is not parallelism
date: 2020-12-05 23:13 +0900
---

```go
go someFunc
```


When you place the `go` keyword in front of a function call, it tells Go to create and execute a brand new go routine, to run the code specifically inside of the given function.

By definition, a go routine is a "separate line of code execution that can be used to handle blocking code".

Given a single CPU, spawning multiple go routines doesn't mean that all of them are being executed at the same time. By default, Go attempts to use only one CPU core, and so it is only running the code inside one of these routines at a time. A Go scheduler monitors this job of cycling through the go routines very quickly to ensure that the program is running efficiently.



This leads to the definition of concurrency; and how it differs from parallelism.

- **Concurrency**: we can have multiple threads executing code. If one thread blocks, another one is picked up and worked on. To put it differently, when you say a program is concurrent, it means that it can run different kinds of things *kind of* at the same time, but not exactly simultaneously (definition from the tutorial).

- **Parallelism**: Multiple threads executing literally simultaneously. Requires multiple CPUs.


<br>
But simply spawning go rountines won't do anything. Without channels, the main go routine will end the program without caring about the active child go routines. A channel is like an instant messaging, in which different go routines communicate with one another. 

How do you implement the channel in the code? Simply pass it into the function. Note that channels are typed. A channel of string type would only accept go routines that exchange string data.

```go
c := make(chan string)

go someFunc(arg, c)

func someFunc(arg string, c chan string) {}
```

<br>
Now, how do you send a message into the channel? 

```go
// To send to the channel
c <- "Message"

// To receive the value from the channel
<- c
```



The program will wait for something to receive from the channel. Using a for loop, we can print out the values that are being passed into the channel. Loop 1 and Loop 2 have slightly different syntax, but they return the same result.

```go
c := make(chan string)

// loop 1
for {
    fmt.Println(<- c)
}

// loop 2
for s := range c {
    fmt.Println(s)
}
```



More on channels later.
