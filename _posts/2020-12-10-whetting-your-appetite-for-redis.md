---
layout: post
title: Whetting your appetite for redis
date: 2020-12-10 22:33 +0900
---
While following through the tutorial series on Koa.js and TypeScript (continued from the [previous post]({% post_url 2020-12-09-koa-very-briefly %}), I ran into the following code snippet:

<br>

```js
export function redisStorage(): Interfaces.IStorage {
  
  const client = redis.createClient(config.redis);

  const rpush = promisify(client.rpush).bind(client);
  const lrem = promisify(client.lrem).bind(client);
  const lrange = promisify(client.lrange).bind(client);

  return {
    get: (list: string) => {
      return lrange(list, 0, -1).then((val: string[]) => val).catch((e: Error) => []);
    },
    add: (list: string, title: string) => {
      return rpush(list, title).then((val: number) => val > 0).catch((e: Error) => false);
    },
    remove: (list: string, title: string) => {
      return lrem(list, title).then((val: number) => val > 0).catch((e: Error) => false);
    }
  }
}
```

<br>

What is this. 

That was my first reaction at the sight of this code. 

To be honest, I had the joy of typing away the whole thing. To have the joy of understanding, though, sustained efforts will be required for the next couple days (or weeks). One thing that's come out of this "typing" exercise was a question about redis, a need to close the gap of knowledge and experience, and what to explore tomorrow. It won't be a streamlined process, but it will be another interesting discovery exercise.