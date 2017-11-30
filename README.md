# Ideaboard Guide - v2

Generate new Rails API app with --api

```ruby
rails new --api ideaboard-api
cd ideaboard-api
```

Generate and run migration:

```ruby
rails g model Idea title:string body:string
rails db:migrate
```

In `db/seeds.rb`, add seeds into `idea` model:

```ruby
puts "creating ideas..."
ideas = Idea.create(
  [
    {
      title: "A new cake recipe",
      body: "Made of chocolate"
    },
    {
      title: "A twitter client idea",
      body: "Only for replying to mentions"
    },
    {
      title: "A novel set in Italy",
      body: "A mafia crime scene"
    }
  ]
)
```

Then run 
```
rails db:seed
```

Create an `IdeasController` with an index action in `app/controllers/api/v1/ideas_controller.rb`

```
module Api::V1

  class IdeasController < ApplicationController

    def index

      @ideas = Idea.all
      render json: @ideas
      
    end

  end

end
```

Add ideas as a resource in `config/routes.rb`:
```
Rails.application.routes.draw do
  namespace :api do
    namespace :v1 do
      resources :ideas
    end
  end
end
```

Run rails server at port 3001:
```
rails s -p 3001
```

When we open `http://localhost:3001/api/v1/ideas`, we should see our data produced in json format:
```
[{"id":1,"title":"A new cake recipe","body":"Made of chocolate","created_at":"2017-11-30T03:59:25.301Z","updated_at":"2017-11-30T03:59:25.301Z"},{"id":2,"title":"A twitter client idea","body":"Only for replying to mentions","created_at":"2017-11-30T03:59:25.323Z","updated_at":"2017-11-30T03:59:25.323Z"},{"id":3,"title":"A novel set in Italy","body":"A mafia crime scene","created_at":"2017-11-30T03:59:25.327Z","updated_at":"2017-11-30T03:59:25.327Z"}]
```
