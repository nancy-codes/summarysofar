---
layout: post
title: The 'Receiver' concept
date: 2020-10-27 18:19 +0900
---
Go doesn't support class-based programming like other OOP languages. Instead, Go allows you to define a new type that "extends" an existing type and add custom methods to the new type. 

For instance, we can create a type called book that is of a struct type with `name` and `author` fields. Then, we can create a method called `print` that logs out book information. Here, a value receiver was used as opposed to a pointer receiver (`*book`) because we want to work with a copy of the original `book` value, not the `book` itself. 

By convention, we use a 1- or 2-letter abbreviation that matches the type of a receiver. In the example below, the receiver is `b`, which serves as an actual copy of the book-type variable. The similiar concept exists in other languages like Ruby (i.e., `self`) and JavaScript (aka, `this`). Note that it is idiomatic to encapsulate new struct creation in constructor functions (aka, `newBookByLewis`).

```go
type book struct {
	title, author  string
}

func newBookByLewis(title string) *book {
	b := book{title: title}
	b.author = "C.S. Lewis"
	return &b
}

func (b book) print() {
	fmt.Printf("%s is authored by %s.\n", b.title, b.author)
}

func main() {
	currentlyReading := newBookByLewis("The Screwtape Letters")
	currentlyReading.print()
}

```