---
layout: post
title: 'Serialization: PORO vs. Model'
date: 2019-10-01 21:36 -0600
---
In Rails, a model talks to a database. It needs a translator that can speak both SQL and Ruby: Active Record. For instance, we have an item model below, which calls an ActiveRecord method `.all` to fetch all rows from the `Item` table.

```ruby
# app/models/item.rb
class Item < ApplicationRecord
  # ApplicationRecord inherits from ActiveRecord
end

# app/controllers/items_controller.rb
class Api::V1::ItemsController < ApplicationController
  def index
    render json: Item.all
  end
end
```

On the other hand, a PORO (which stands for Plain-Old-Ruby-Object) is database-independent (hence, PORO does not inherit from ActiveRecord). It can instantiate an item object, which is intended to be used temporarily: **it does not need to be stored.** In the context of a JSON API, say a weather API, we can consume data and manipulate it in many different ways, but they don't need to persist in a database. What's the use of holding onto temporary data? In this case, we can pass in a PORO instead of a model to a serializer.
