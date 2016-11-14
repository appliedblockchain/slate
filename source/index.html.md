---
title: API Reference

language_tabs:
  - shell
  - ruby
  - python
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Kittn API! You can use our API to access Kittn API endpoints, which can get information on various cats, kittens, and breeds in our database.

We have language bindings in Shell, Ruby, and Python! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

This example API documentation page was created with [Slate](https://github.com/tripit/slate). Feel free to edit it and use it as a base for your own API's documentation.

# Authentication

> To authorize, use this code:

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
```

> Make sure to replace `meowmeowmeow` with your API key.

Kittn uses API keys to allow access to the API. You can register a new Kittn API key at our [developer portal](http://example.com/developers).

Kittn expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: meowmeowmeow`

<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal API key.
</aside>

# User

## Get current user

```shell
curl -H "Content-Type: application/json" http://localhost:3000/api/user
```

> The above command returns JSON structured like this: 

```json 
{
  "status": 200,
  "message": "success",
  "data": {
    "id": 1,
    "first_name": "Jane",
    "last_name": "Doe",
    "username": "janedoe",
    "email": "janedoe@example.com",
    "mobile": "+44 123 456 7890",
    "groups": null,
    "image": "1",
    "public_key": "04fda237628f0a6a5c71a40d05b66bf07662b61b030149669cd7038f83fab848a1b6f3f7d154e52af9d4e9dc6f04ce029f39755996d656dcfc2266e7d75d05c6fe"
  }
}
```

This endpoint returns the current user 

### HTTP Request

`GET http://localhost:3000/api/user`


## Create a user

```shell
curl -H "Content-Type: application/json" -X POST -d '
{
  "first_name": "Bob",
  "last_name": "Jones",
  "mobile": "01234343",
  "username":"steve",
  "email":"steve@example.com"
}' 
http://localhost:3000/api/user
```

> The above command returns JSON structured like this:

```json
{
  "status": 200,
  "message": "success",
  "data": {
    "id": 11,
    "first_name": "Bob",
    "last_name": "Jones",
    "username": "steves",
    "email": "steve@example.com",
    "mobile": "01234343",
    "groups": null,
    "image": null,
    "public_key": null
  }
}
```

This endpoint creates a new user

### HTTP Request

`POST http://localhost:3000/api/user`

### Query Parameters

Parameter | Default | Required | Description
--------- | ------- | ---------| -----------
first_name | n/a | Yes | User's first name
last_name | n/a | Yes |  User's last name
mobile | n/a | Yes | User's mobile telephone number
username | n/a | Yes | Requested username (Must be unique)
email | n/a | Yes | User's email address (Must be unique)


# Kittens

## Get All Kittens

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let kittens = api.kittens.get();
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all kittens.

### HTTP Request

`GET http://example.com/api/kittens`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

