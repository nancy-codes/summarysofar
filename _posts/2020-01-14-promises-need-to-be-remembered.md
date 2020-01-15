---
layout: post
title: Promises need to be remembered
date: 2020-01-14 20:25 -0700
---
"What is a promise?"

This was a question from one of those mock interviews that met with an awkward silence.

I tinkered with it in my projects, even blogged about it, but I could not give a sound answer to this technical question. It totally slipped my mind! My mind was so befuddled in that I could not even make up an answer. Thank God it was a mock interview.

This mildly humiliating incident prompted me to look for a stack of flashcards. They were proven study methods to make those concepts stick in your mind.

Sadly, the flashcards did not exist in my coding journey. It didn't occur to me to sit down, make a list of words, and assign a card to each word. Consequently, my unwillingness to take some time to run through important vocabulary led to an amnesiac state of mind; and a loss of an opportunity.

To fix this issue, I decided to build a simple node API to systemize a learning process. The API would consist of two endpoints (posting a new card and getting all cards), like so:

![dev_lingo](https://user-images.githubusercontent.com/24424825/72402400-62815600-370c-11ea-80b7-2fb315124db4.png)

But the challenging part was connecting an HTML form and express routes. I ran into an issue in which a post request would return a response body that is empty (aka, { }). Somehow the form input didn't get passed securely from a controller action to the post route. To add to the confusion, the same thing worked fine in Postman.

Long story short (~2 hours of digging stack overflow), I was informed by an anonymous person who had exactly the same question. The missing piece was a `name` attribute within the `input` elements that would comprise the keys of a response `body` object. Furthermore, a deep search into form handling in node revealed more interesting stuff like validation and sanitization of input data.

```
<div class="form-group">
  <label for="term">Term</label>
  <input class="form-control" id="term" name="term">
</div>
```

Anyhow, the chaotic process of searching is normal in web development. It's tempting to give up the search and make it sour grapes; but if you hold on to the promise, then things will work out eventually.
