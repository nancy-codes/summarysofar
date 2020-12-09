---
layout: post
title: Koa, very briefly
date: 2020-12-09 13:53 +0900
---

A short break from Go. In the meantime, let's redirect our attention to Node.js. 

With Express, you can make a simple web server in four lines.

```js
const express = require('express')
const app = express()
app.get('/', (req, res) => { res.send('Hi!') })
app.listen(3000, () => { console.log('Server Ready') })
```



Same thing with Koa, which is more light-weight than Express. Koa unpacks the low-level implementations done by Express in just 4 lines.


```js
const Koa = require("koa");
const app = new Koa();

const Router = require("koa-router");
const router = new Router();

router.get(`/`, async (ctx) => {
  try {
    ctx.body = "Hi!";
  } catch (err) {
    console.error(err);
  }
});

app.use(router.routes());

app.listen(3000, async () => {
    console.log("Server listening on port 3000");
  })
  .on("error", err => {
    console.log(err);
  });
```

As you can see, everything is all over the shop in the above code. But these middlewares and routes can be, and should be extracted out to separate directories to modularize the app.


To summarize the major differences between Express and Koa:

- Promises-based control flow, with error handling through try/catch
- Node's request/response objects are wrapped into a single object called `ctx` for context.
- Koa is less reliant on middlewares. It starts with the bare minimum essentials (middleware kernel), and you can add your own as you go.
- No built-in routing. But there are third-party libraries that can help you implement them in your app.


<br>
**References**
- [Koa vs. Express](https://github.com/koajs/koa/blob/master/docs/koa-vs-express.md)