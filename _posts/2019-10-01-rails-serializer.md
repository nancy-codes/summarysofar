---
layout: post
title: Rails serializer
date: 2019-10-01 20:44 -0600
---

In the context of Rails API, we begin to talk about a serializer. It is a data-formatting layer that acts like a **view** in the traditional MVC framework.

Let's say a client or a server makes an HTTP GET request to our Rails API with the following endpoint:

```
get '/api/v1/items'
```
For organization's purposes, endpoints are namespaced so that APIs are taken care of separately from controllers. Additionally, versioning is also namespaced. Each namespace gets a subfolder under the `controllers` directory in a Rails app (see below).

![namespaced_api](https://user-images.githubusercontent.com/24424825/66015192-dade4700-e48e-11e9-9d67-3ae0265528d3.png)

In our routes file, a specific verb + endpoint combo is mapped to a specific controller action; in our simple example, an index action. A `resources` syntax comes handy in generating a list of RESTful routes and route_helpers.

```ruby
# routes.rb
Rails.application.routes.draw do
  namespace :api do
    namespace :v1 do
      resources :items, only: [:index]
    end
  end
end

```

Within the index action, we call `render json:`, which is a built-in rails method that takes 2 steps under the hood: 1) data prep and 2) json encoding. In the first step, `render json:` calls `.as_json` method that formats a json structure. Then, in the second step, it calls `.to_json` method that turns a formatted object into a string.

```ruby
class Api::V1::ItemsController < ApplicationController

  # without serializer
  def index
    render json: Item.all
  end

  # with serializer
  def index
    render json: ItemSerializer.new(Item.all)
  end

end
```

Now, I've mentioned earlier that a serializer is a data-formatting layer. By data-formatting, it means that data can be displayed partially (or selectively). In other words, the serializer allows us to modify our object during our data prep phase, so that we can customize what data we want to send back in a response. The serializer takes in the entire class (i.e., `Item.all`) and returns an array of altered hashes containing certain attributes.

There is a cool gem called `fast_jsonapi`, made by Netflix. Basically it puts a json in a specific format so that it's more readable. With this gem installed in our app, we can generate a serializer from the command line. Specify a model name and whichever attributes you want to select and display.

```
$ rails g serializer <model_name> <attribute_1> <attribute_2>
```

Running the command will result in the creation of a brand new serializer folder with an `item_serializer.rb` file. Furthermore, a custom attribute (i.e., `greeting`) can be added as shown below.

```ruby
class ItemSerializer
  include FastJsonapi::ObjectSerializer
  attributes :id, :name, :description, :unit_price, :merchant_id

  attribute :greeting |object| do
    "Item #{object.name} is great!"
  end
end
```

Back to the controller. Before rendering a response, we can pass in `Item.all` to a serializer and control what we choose to show (and not to show). Isn't this cool?!
