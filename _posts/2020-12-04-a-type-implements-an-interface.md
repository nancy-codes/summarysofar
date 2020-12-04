---
layout: post
title: A type implements an interface
date: 2020-12-04 10:36 +0900
---

It will take a while to warm up to the concept of interfaces in Go. To get a better sense of it, we can work on a simple program that utilizes interfaces. Below are my notes from [this go tutorial](https://www.udemy.com/course/go-the-complete-developers-guide) provided by Udemy. While learning about how interfaces work, we are also learning how to navigate the standard documentation around built-in packages and methods.

<br>
```go
package main

import (
	"fmt"
	"net/http"
	"os"
)

func main() {
	resp, err := http.Get("http://google.com")

	if err != nil {
		fmt.Println("Error: ", err)
		os.Exit(1)
	}

	bs := make([]byte, 99999)

	resp.Body.Read(bs)
	fmt.Println(string(bs))
}
```


In `net/http` package, the function `Get` accepts two arguments. First one is a pointer to a Response struct that contains header and body information; the second argument is error. 



```go
func (c *Client) Get(url string) (resp *Response, err error)
```



Probing into the documentation around the Get function, we can see that the Response struct has a field called `Body`, which is something of type `io.ReadCloser`. 



```go
type Response struct {
    Status     string
    StatusCode int
    ...
    Body io.ReadCloser
    ...
}
```



Further digging reveals that `ReadCloser` is of interface type that groups Read and Close methods. The `Body` implements the `Reader` interface, and thus it has access to the `Read` and `Close` methods.

```go
type ReadCloser interface {
    Reader
    Closer
}
```



By convention, the naming of the function within the interface has a suffix of `er`. The `Reader` interface is a common medium from which the output of the same type  - byte slice ([]byte) - is returned. The `Read` function will read raw source of data into a byte slice of arbitrarily large size.


```go
type Reader interface {
    Read(p []byte) (n int, err error)
}
```


```go
bs := make([]byte, 99999)

resp.Body.Read(bs)
fmt.Println(string(bs))
```



Now, the above code can be trimmed down into a single line like so:



```go
io.Copy(os.Stdout, resp.Body)
```



How does the `Copy` function in the package `io` work? It requires two arguments, and each one has to be of a particular interface type: Writer and Reader interface, respectively.

The first argument in the example is `os.Stdout`, which is a value of type `File`. Looking at the standard documentation around it, we know that `File` has a function called `Write` defined on it. Meaning, the `os.Stdout`, of file type, implements the Writer interface. 

The second argument in the example is `resp.Body`. From the previous example, we know that this value implements Reader interface. 


```go
func CopyBuffer(dst Writer, src Reader, buf []byte) (written int64, err error)
```


The `Copy` function passes these two arguments into another function inside called `CopyBuffer` that reads the source data into a buffer, which is essentially a byte slice big enough to contain the read data, and write to standard output.

More on the interfaces later.
