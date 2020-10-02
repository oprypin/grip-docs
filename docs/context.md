Context is a class which contains the Request, Response structures of an HTTP server, since Crystal Language allows us to extend its core features we have decided to add couple of helper functions to the context class.

## Available methods

[`delete_req_header/1`](#delete_req_header)
[`delete_resp_header/1`](#delete_resp_header)
[`get_req_header/1`](#get_req_header)
[`get_resp_header/1`](#get_resp_header)
[`halt/0`](#halt)
[`merge_resp_headers/1`](#merge_resp_headers)
[`put_req_header/2`](#put_req_header)
[`put_resp_header/2`](#put_resp_header)
[`put_status/1`](#put_status)
[`send_resp`/1](#send_resp)
[`json/1`](#json)
[`html/1`](#html)
[`text/1`](#text)
[`binary/1`](#binary)
[`fetch_json_params/0`](#fetch_json_params)
[`fetch_query_params/0`](#fetch_query_params)
[`fetch_body_params/0`](#fetch_body_params)
[`fetch_file_params/0`](#fetch_file_params)
[`fetch_path_params/0`](#fetch_path_params)

### delete_req_header

Deletes a request header if present.

```ruby
def get(context)
  context
    .delete_req_header("Referer")
    .text(nil)
end
```

### delete_resp_header

Deletes a response header if present.

```ruby
def get(context)
  context
    .json("Hello, World!")
    .delete_resp_header("Content-Type")
end
```

### get_req_header

Returns the values of the request header specified by `key`.

```ruby
def get(context)
  referer =
    context
      .get_req_header("Referer")

  context
    .json(
      {
        "referer" => referer
      }
    )
end
```

### get_resp_header

Returns the values of the response header specified by `key`.

```ruby
def get(context)
  content_type =
    context
      .get_resp_header("Content-Type")

  context
    .json(
      {
        "contentType" => content_type
      }
    )
end
```

### halt

Halts the function chain by closing the response stream.

```ruby
def get(context)
  context
    .json("Hello, World!")
    .halt
end
```

### merge_resp_headers

Merges a series of response headers into the context.

```ruby
def get(context)
  context
    .merge_resp_headers({"Content-Type" => "application/json"})
    .send_resp("Hello, World!")
end
```

### put_req_header

Adds a new request header `(key)` if not present, otherwise replaces the previous value of that header with `value`.

```ruby
def get(context)
  context
    .put_req_header("Referer", "www.google.com")
    .json("Hello, World")
end
```

### put_resp_header

Adds a new response header `(key)` if not present, otherwise replaces the previous value of that header with `value`.

```ruby
def get(context)
  context
    .put_resp_header("Content-Type", "application/json")
    .send_resp("Hello, World!")
end
```

### put_status

Assigns the given status code to the context response.

```ruby
def get(context)
  context
    .put_status(400)
    .json("Bad request")
end
```

### send_resp

Sends a response to the client.

```ruby
def get(context)
  context
    .send_resp("Hello, World!")
end
```

### json

Sends JSON response.

```ruby
def get(context)
  context
    .json("Hello, World!")
end
```

### html

Sends HTML response.

```ruby
def get(context)
  context
    .html("Hello, World!")
end
```

### text

Sends text response.

```ruby
def get(context)
  context
    .text("Hello, World!")
end
```

### binary

Sends binary response.

```ruby
def get(context)
  context
    .binary("Hello, World!")
end
```

### fetch_json_params

Fetches JSON parameters from the JSON parser.

```ruby
def get(context)
  params =
    context
      .fetch_json_params

  context
    .json(params)
end
```

### fetch_query_params

Fetches query parameters from the query string.

```ruby
def get(context)
  params =
    context
      .fetch_query_params

  context
    .json(params)
end
```

### fetch_body_params

Fetches body parameters from the body parser.

```ruby
def get(context)
  params =
    context
      .fetch_body_params

  context
    .json(params)
end
```

### fetch_file_params

Fetches file parameters from the file parser.

```ruby
def get(context)
  params =
    context
      .fetch_file_params

  context
    .json(params)
end
```

### fetch_path_params

Fetches path parameters from the path parser.

```ruby
def get(context)
  params =
    context
      .fetch_path_params

  context
    .json(params)
end
```