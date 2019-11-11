---
layout: post
title: Processes in a Procfile
date: 2019-11-11 09:51 -0700
---
During my web development process, I've encountered many files with a suffix, `-file`. Gemfile, Rakefile, Pipfile, Dockerfile, Procfile, just to name a few. Today, I'm going to focus on just one of them, `Procfile`, which goes hand in hand with Heroku.

As the name suggests, the file exists to specify process types and bundle them together in one place. An application may consist of several processes. The most basic one would be a web server. Additionally, there may be background workers, such as sidekiq. What do you do with these process types? You specify the pre-defined name of each process (i.e., web, worker, clock, etc) and pair it with a specific command, like so:

```ruby
# ./Procfile
web: bundle exec rails server -p $PORT
worker: bundle exec sidekiq
```

Heroku allows you to configure a 'production-like' environment locally. So you can `$ heroku local` to see if your app is running okay without having to visit `your-app-name.herokuapp.com`. Often, environment (ENV) config variables need to be set up on heroku dashboard. For instance, any sensitive information or key-value pairs that you would put in an  `application.yml` file should also be present in production environment.

To mimic this action of config vars while testing your app locally, you can do a similar setup with an `.env` file. Just like `application.yml`, you want to keep this file private, so don't forget to add that to `.gitignore`. Heroku lessens the burden of typing out everything (or a series of copy-and-pasting), by letting you import the entire list of config variables from remote heroku to local environment, with the following command:

```ruby
$ heroku config:get CONFIG-VAR-NAME -s  >> .env
```

Additionally, there is a cool Procfile manager called [foreman](https://ddollar.github.io/foreman/). It allows you to cherry-pick a single process type to run locally. So if you want to just run a background worker, you can `$ foreman start worker`. Alternatively, there is another tool called [Overmind](https://medium.com/reflektive-engineering/organize-your-development-processes-with-overmind-21719a0210e1), which aims to solve Procfile-related pain points that I haven't run into yet. I'll cross that bridge when I come to it.
