---
layout: post
title: Understanding web APIs with verbs
date: 2019-10-10 20:36 -0600
---
An API stands for _Application Programming Interface_. Assuming that it's your first time hearing this word, what do you think it does? Inferring from the three words, an API sounds like a meeting place where two or more **apps** come together and interact in some ways.

That's a loose description of API, but still it's vague and feels so foreign (at least to me). When I'm trying to learn something new, and it doesn't click, I tend to turn to **verbs** associated with the thing. It's almost like playing a game of Who Am I to guess the identity of something. In the context of APIs, it's helpful to define them by what they do.

So, here is a list of verbs that go together with APIs:
- Build
- Consume
- Query
- Parse
- Namespace
- Version (v.)

Just by looking at these verbs, you get a sense that an API is a thing that can be built, consumed, queried, parsed, and namespaced. (Not quite, but close.)

It also helps to understand something by negation; that is, knowing what something is not. In the case of an API, it is neither a server nor a database. An API is more like a middleman (in the form of the code) that governs the relationships of those servers and databases. By "building" an API, it means that we are setting up a middleman that could receive a request from one app and pass it to the other app, which will process that request and return some kind of response to the first app through the middleman.

Versioning comes into play when building an API. When we're storing data that are dynamic in nature, we need a way to keep different versions of data. Without such versioning system, we will lose access to a rich repository of data from older versions. We wouldn't want that to happen in our app. So what should we do?

We can add a versioning layer like `V1` or `V2` with namespacing. It is basically a partitioning of the code, or a design pattern that imposes order on the structure of an app to make it extensible.

Besides versioning, namespacing bestows a single responsibility to each controller (aka, a skinny controller that contains only a couple of actions). With namespacing, when some part of the code needs to change, we can narrow our focus and only touch the relevant file(s). In other words, namespacing creates super-specific entry points to the application of interest. So when some app is querying a certain piece of data, the request will trigger a super-specific controller action.

Lastly, where does the verb 'Parse' come into play? It has to do with a response object that is tossed around from the provider to the client. The app on the receiving end finds it easy to work with hashes, rather than JSON objects (Unparsed data are just messy).

So that's it for the intro to web APIs. Without coding in real time, this blog post would make little sense to you. So I highly encourage you to play around with some popular [APIs](https://www.programmableweb.com/news/10-most-popular-database-apis/brief/2019/05/06)!
