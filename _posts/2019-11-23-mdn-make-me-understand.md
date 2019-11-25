---
layout: post
title: MDN, make me understand
date: 2019-11-23 20:20 -0700
---
Recently, I was introduced to the idea of Promise (with a capital P). As with most things, a promise was invented by necessity. It solved the problem of dealing with multiple layers of callbacks (aka, callback hell). Promises handle this seemingly endless chain of function calls a lot more gracefully.

![callback-hell](https://image.slidesharecdn.com/promisesandchaininginangularjs-141027044455-conversion-gate02/95/promises-and-chaining-in-angularjs-into-callback-hell-and-back-again-17-638.jpg?cb=1414385382)
Image source: [slideshare](https://www.slideshare.net/HansGuntherSchmidt/promises-and-chaininginangularjs)

**A brief recap**: a callback is a function that gets passed into another function as a parameter and is expected to be invoked by a lower-level function, either immediately (synchronous) or some time later (asynchronous). In other words, you can create a callback function and provide it to another function, but you won't call it directly in your code.

According to [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises), a promise is an object that has one of the three states: pending, fulfilled, or rejected. To this promise object, a callback function can be attached. Usually two callbacks are chained: `.then()` for a successful async request, and `.catch()` for a failed request. A normal function can be wrapped in a Promise and be attached to these callbacks. The `then-catch` syntax makes it easier for human developers to follow the sequential logic.

```javascript
// a normal function
function findBook(id, onSuccess, onFailure) {
  $.getJSON({
    url: `some_book_api/${id}`,
    success: onSuccess,
    error: onFailure
  })
}

// turns into a promise
function findBook(id) {
  return new Promise((resolve, reject) => {
    $.getJSON({
      url: `some_book_api/${id}`,
      success: resolve,
      error: reject
    })
  })
}
```

Invoking the second `findBook` function will return a promise, which can go to either `.then()` or `.catch()` routes. Note that `.then` and `.catch` themselves return a promise, which can be attached to another chain of promises (indefinitely until it hits an error condition). Now that we have a promise rather than a passed-in callback, we can refactor the code as follows:

```javascript
// callbacks
findBook(1, (book) => {
  findReviews(book, (reviews) => {
    updateUI({
      book,
      reviews: reviews.query.results
    })
  }, showError)
}, showError)

// promises
findBook(1)
  .then(findReviews)
  .then((data) => updateUI(data))
  .catch(showError);
```

The promise-based code is much more readable. But refactoring can continue. `findBook` function can be wrapped in another function that utilizes JavaScript's built-in await-async feature. With await-async, roughly three things need to change:

1. Prepend an outer function with a keyword `async`; prepend all inner functions within `try` block with a keyword `await`.
2. Use `try-catch` block to handle error, instead of attaching `.catch()` to the function call.
3. Since this function itself returns a promise, it still needs to be attached to `.then` to be able to access the returned value of the function.

```javascript
async () => {
  try {
    const book = await findBook(1)
    const reviews = await getReviews(book.reviews)

    updateUI({
      book,
      reviews,
    })
  } catch (e) {
    showError(e)
  }
}
```



**References**
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises
- https://tylermcginnis.com/async-javascript-from-callbacks-to-promises-to-async-await/
