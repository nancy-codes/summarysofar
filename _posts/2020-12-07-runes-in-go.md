---
layout: post
title: Runes in Go
date: 2020-12-07 14:15 +0900
---
Given finite resources, what is the best way to learn a new language? From personal experiences, it is effective to learn directly from an example. For instance, if you want to understand how a certain verb, like `run`, is used within a sentence, it is best to learn from a full sentence.  

So you're learning a programming language, and one day you encounter some vocabulary that are new to you. For instance, I learned about `rune` while learning Go. The word `rune` appears in the context of encoding.



So, let's look at the example below.

```go
package main

import "fmt"

func SwapRune(r rune) rune {
    switch {
    case 97 <= r && r <= 122: // case 'a' <= r && r <= 'z':
        return r - 32
    case 65 <= r && r <= 90: // case 'A' <= r && r <= 'Z':
        return r + 32
    default:
        return r
    }
}

func main() {
    var result string
    m := "Christmas"
    for _, c := range m {
      result += string(SwapRune(c))
    }
    fmt.Println(result)
}
```



In order to comprehend what's going on here, we first need to understand how character encoding works. In a question format, "how do you map a character "A" into a number that a computer can understand?"

A couple of systems have been invented to solve the problem of representing characters in binary formats and storing a string of Unicode code points in memory. Those systems include ASCII, Unicode, and UTF-8 (UTF: Unicode transformation formats).

A code point is simply a number with meaning imposed by the Unicode standard. It can be stored in many different formats (UCS-2, UTF-8, UTF-7, etc).

For instance, the English letter A would be **U+0041**, in decimal it would be 65. The lowercase a is 97. In the diagram below, the uppercase and lowercase characters are two rows apart in a 16x16 table. A more complex symbol, like 💚 (GREEN HEART), would be **U+1F49A**. 

![ascii table](/assets/images/ascii.png)


<br>
So, what is rune?

By standard definition, "`rune` is an alias for `int32` value that represents a single Unicode code point." (from [golang doc](https://golang.org/doc/effective_go.html#introduction)) 

Note the word "single". If you pass in a string of letters, like `SwapRune("Christmas")`, a compile error will be thrown. 

If we run the script above, we get the following output. Each letter in the string  `Christmas` was passed into the `SwapRune` function, which emits the opposite case.

```
➜ go run rune.go
cHRISTMAS
```



A more compact way to code out the same logic, with the help of the `strings` package:

```go
package main

import (
	"fmt"
	"strings"
)

func main() {
	rot13 := func(r rune) rune {
		switch {
		case r >= 'a' && r <= 'z':
			return r - 32
		case r >= 'A' && r <= 'Z':
			return r + 32
		}
		return r
	}
	fmt.Println(strings.Map(rot13, "Christmas"))
}
```



<br>

#### References

- https://www.joelonsoftware.com/2003/10/08/the-absolute-minimum-every-software-developer-absolutely-positively-must-know-about-unicode-and-character-sets-no-excuses/
- https://blog.golang.org/strings

