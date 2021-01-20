---
layout: post
title: A little bit about TypeScript
date: 2021-01-20 17:35 +0900
---

Suppose you have a function, and you pass in an array of numbers or a string.

The function would return the output values in ascending order or in alphabetical order, respectively.

In TypeScript, you can specify that an input collection can be of type an array of numbers or a string. That "or" is implemented with a union operator (`|`).

```js
class Sorter {
  constructor() {public collection: number[] | string }
}
```

However, the union operator comes with some restrictions. The collection is now limited to a narrower list of methods common to both arrays and strings.

For instance, with the union operator, the collection would lose access to indexing and mutating an object. This is because arrays are mutable while strings are immutable in JavaScript.

```js
arr = [1, 2, 3];
arr[0] = 5;
arr
> [5, 2, 3]

str = 'hello';
str[0] = 'y';
str
> "hello"
```

How can we fix this such that the collection can behave differently based on the input data type?

This is where type guards come into play. 

A trivial example of a type guard:

```js
class Sorter {
  constructor() {public collection: number[] | string }

  sort(): void {
    const { length } = this.collection.length;

    // Bubble Sort algorithm uses two nested for loops.
    for (let i = 0; i < length; i++) {
      for (let j = 0; j < length - i - 1; j++) {
        if (this.collection instanceof Array) {
          this.collection // array methods are restored
        }

        if (typeof this.collection === 'string') {
          this.collection // string methods are restored
        }
      }
    }
  }
}
```

Adding a conditional block (or a type guard) lifts the restrictions imposed by the union operator. That is, you can convince TypeScript that this collection in this particular context should have access to properties and features that are specific to this type.

#### References

- [Type Guard](https://basarat.gitbook.io/typescript/type-system/typeguard)