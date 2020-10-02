The routing mechanism is based on `Kemal` which uses the radix tree implementation to identify the URL patterns.

```ruby
class DemoController < Grip::Controllers::Http
  def index(context)
    context
      .json(nil)
  end
end

class Application < Grip::Application
  def initialize
    # The routing occurs via the `get` macro which instantiates the controller class and assigns a route
    # to the routing mechanism.
    #
    # `GET /` -> CLIENT -> SERVER -> ROUTER -> ROUTE -> CONTROLLER -> index/1
    #
    get "/", DemoController, override: :index
  end
end
```