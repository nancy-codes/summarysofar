---
layout: post
title: Rendering lists
date: 2020-12-25 18:24 +0900
---

Imagine fetching a list of users randomly from the [API]('https://jsonplaceholder.typicode.com/users') as shown below. Which syntax do you prefer?
<br /><br />

<img src="/assets/images/random_users.png" alt="users list" width="300" />

<br />
#### Bottle, template, and Requests

```python
# main.py
from bottle import Bottle, route, run, template
import requests


@route("/")
def index():
    users = (requests.get("https://jsonplaceholder.typicode.com/users")).json()
    output = template("users", users=users)
    return output


run(host="localhost", port=8080, debug=True)

# users.tpl
<ul>
  %for u in users:
    <li id={{ u["id"] }}>{{ u["name"] }}</li>
</ul>
```

<br />
#### Sinatra, ERB, and Faraday

```ruby
# app.rb
require 'sinatra'
require 'faraday'

URL = 'https://jsonplaceholder.typicode.com/users';

get '/' do
  response = Faraday.get(URL)
  users = JSON.parse(response.body)
  erb :index, :locals => { :users => users }
end

# views/index.erb
<ul>
  <% users.each do |u| %>
  <li id=<%= u["id"] %>><%= u["name"] %></li>
  <% end %>
</ul>
```

<br />
#### React, JSX, and Axios

```js
// App.js
import React from "react";
import { axios } from "./axios";
const { useState, useEffect } = React;

const URL = "https://jsonplaceholder.typicode.com/users";

const App = () => {
  const [users, setUsers] = useState([]);

  useEffect(() => {
    const fetchUsers = async () => {
      const { data } = await axios.get(URL);
      setUsers(data);
    };

    fetchUsers();
  }, []);

  const renderedUsers = users.map((user) => {
    return <li key={user.id}>{user.name}</li>;
  });

  return <ul>{renderedUsers}</ul>;
};

export default App;

// axios.js
const axios = {
  get(url) {
    return fetch(url)
      .then((res) => res.json())
      .then((d) => ({ data: d }));
  },
};

export { axios };
```
