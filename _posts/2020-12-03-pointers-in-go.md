---
layout: post
title: Pointers in Go
date: 2020-12-03 12:24 +0900
---

Go is a "pass-by-value" language. By that it means, whenever a value is passed into a function, Go copies that value and makes it available to the code inside the function.

This feature can cause problems. For instance, when you need to update an instance of a struct. Let's look at the example below. A person struct has two fields, `firstName` and `lastName`. There are two functions, `updateName` and `print`, which accept a person-type variable as a receiver. 

- `updateName` function modifies the `firstName` field of a given person
-  `print` function prints out all the fields and corresponding values of a given person.

<br>

```go 
package main

import "fmt"

type person struct {
	firstName string
	lastName  string
}

func main() {
	var alex person

	alex.firstName = "Alex"
	alex.lastName = "Kim"
  
  alex.updateName("Jim")
	alex.print()
}

func (p person) updateName(newFirstName string) {
	p.firstName = newFirstName
}

func (p person) print() {
	fmt.Printf("%+v", p)
}
```



```
$ go run main.go
{firstName:Alex lastName:Kim contact:{email: zipCode:0}}
```


Apparently, the `updateName` function doesn't seem to have been applied to the `alex` struct. The first name is still printed as `Alex`, not `Jim`. This is the aforementioned issue caused by the "Pass-by-value" feature in Go. The problem arises because the `updateName` function has been applied to a copy of alex; hence, the changes are not reflected in the originaln alex. 

Here is where pointers come into play. Update the code as below.

```go
...
func main() {
	var alex person

	alex.firstName = "Alex"
	alex.lastName = "Kim"
  
  // Get the memory address from alex
	alexPointer := &alex
	alexPointer.updateName("Jim")
	alex.print()
}

func (pointerToPerson *person) updateName(newFirstName string) {
  (*pointerToPerson).firstName = newFirstName
}
```


Create a pointer variable called `alexPointer` and call the function on it. Change the receiver type of `updateName` function from `person` to `*person`, then replace p with `*pointerToPerson` in the function body. This will turn the pointer `pointerToPerson` into a value type and then update it.

- & (ampersand) operator tells Go to give the memory address of the value that a struct is pointing at.
- *(star) operator tells Go to give the value that this memory address is pointing at.



But there are two * operators that need to be clarified here. * can come in front of either a **type** or a **memory address**.

- When a star operator is used in the receiver function (i.e., `*person`), it is a type description. It means that we're working with a pointer to a given type. 
- When a star operator used in the code inside a function (i.e., `*pointerToPerson`), it is an operator. It means that we want to manipulate the value that the pointer is referencing.


<br>

```go
func main() {
  alex := person{firstName: "Alex", lastName: "Kim"}
  alex.updateName("Jim")
	alex.print()
}

func (pointerToPerson *person) updateName(newFirstName string) {
  (*pointerToPerson).firstName = newFirstName
}
```

Notice above, that as long as the pointer is specified in the `updateName` function, Go allows you to call that function on the original struct. Here, Go will automatically assume that even though `alex.updateName()` is using a value type in the main function, we probably meant to pass in a pointer to the `alex` struct.


Lastly, there is one big edge case regarding the pointers. When we're dealing with slices as opposed to structs, Go doesn't require the explicit use of pointers. This is because whenever a slice is created, Go creates a slice data structure, which has the length capacity and a pointer to an array in one address in memory. The underlying array is created and stored in a completely different adress in memory.

```go
func updateSlice(s []string) {}
```

Go is still behaving as a pass-by-value language when we call a function and pass a slice into it. That is, Go creates a copy of the slice data structure at another address. However, that redundant slice is pointing at the same underlying array in memory. This is why the slice is modified when the `updateSlice` function is called on it.
