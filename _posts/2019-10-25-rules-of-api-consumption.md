---
layout: post
title: Rules of API consumption
date: 2019-10-25 20:00 -0600
---

In the past few weeks, I've been playing around with a number of APIs, including:

- [Propublica API](https://projects.propublica.org/api-docs/congress-api/members/#lists-of-members), to get a list of congress members' data
- [Harry Potter API](https://www.potterapi.com/), to get a list of students from the exclusive 'Order of the Phoenix' society from one of Hogwarts House
- [The National Renewable Energy Laboratory (NREL) API](https://developer.nrel.gov/docs/transportation/alt-fuel-stations-v1/nearest/), to get the nearest alternative fuel station
- [Google directions API](https://developers.google.com/maps/documentation/directions/start), to get the distance/duration between locations

Through these (toy) projects, I've learned how to communicate with APIs. If you're like me, the more you spend time with them, the more you'll realize just how vast the universe of APIs are. There are lots and lots of APIs out there for you to explore, so find one that's interesting to you and create a new project out of it!

Before I get too carried away, let's get back to the learning goals. I'm going to recycle Harry Potter API for this post to demonstrate how to consume it in a Rails app. Here is a general workflow.

---
##### Step 1. Read the docs (and get an API key)
Visit the website. Read the documentation thoroughly. Your app is consuming the API; you are consuming the docs. To get an API key (which is usually a string of alphanumeric characters), you may need to register. Then, you will need to put that in your app. The key should be kept private, never to be hardcoded. How to make it only visible to you? Run the following command in the terminal, and you will find a safe place to store the key.

```
$ bundle exec figaro install
> create config/.application.yml
> create .gitignore
```

```ruby
# config/.application.yml
api_key: some_computer_gibberish
```

Two files are generated. `.application.yml` and `.gitignore`. Both are prefixed with a dot, indicating that they are hidden files. Once the key is saved in the yml file, an environment variable (aka, `ENV['some_name']`) is used to add this secret piece of data within your app. For instance, when you are creating a Faraday object to make an HTTP request, you need to pass in the secret API key, either within the headers or the parameters, like so:

```ruby
def conn
  Faraday.new(:url => 'path_to_api') do |faraday|
    faraday.request  :url_encoded             # form-encode POST params
    faraday.adapter  Faraday.default_adapter  # make requests with Net::HTTP
    faraday.params["A"] = ENV['B']
  end
end
```

Here, "A" is defined by the API doc (why we are told to peruse the doc). "B" is what you define in the `.application.yml`. In the above example, "B" would be "api_key".


---
##### Step 2. Write a feature test
Now, it is time to TDD the features that you expect to see in your app from the user's perspective. Imagine a scenario in which the user visits your web application, sees a dropdown menu of options, selects one, clicks a submit button, and sees some texts on the page (i.e., the information that he/she is looking for). A user story contains the details of the scenario, and we as developers are to follow it as exactly and thoroughly as possible.


---
##### Step 3. Read the errors (several times)
Red error messages should not make you upset in any way. Rather, you should treat them like a guide who will lead you to the next step. In the case of consuming an API, you will find that there is an implicit order in TDD-ing. With enough practice, you might be anticipating a set of actions and half tempted to implement them far in advance, like so:

- Add controller
- Add action view page (iterate over a local variable, `facade`)
- Add facade (initialize with an HTTP request)
- Within facade, format json response and make an object out of it
- Refactor facade with services (TDD these services)
- Final touch (make views aesthetically pleasing)


But this is considered bad practice, doing things without being told. Just keep this workflow in mind and follow one error at a time (like you've read it for the first time!).
