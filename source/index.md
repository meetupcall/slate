---
title: API Reference

language_tabs:
  - shell
  - ruby

toc_footers:
  - <a href='mailto:simon.moxon@meetupcall.com'>Request an API Key</a>

includes:
  - errors

search: true
---

# Introduction

```ruby
# A Ruby/Rails client can use a simple class like this to consume our API:

class SignupClient
  include HTTParty
  base_uri 'https://manage.meetupcall.com/api/v1'
  format :json

  def initialize(api_key)
    @options = { :headers => {
                'Content-Type' => 'application/json',
                'Accept' => 'application/json',
                'x-api-key' => api_key }
               }
  end

  def create(params)
    self.class.post '/signups', @options.merge(body: params.to_json)
  end

  def index
    self.class.get '/signups', @options
  end

  def get(email)
    self.class.get "/signups/#{email}", @options
  end
end
```

Welcome to alpha version Meetupcall V1 API. You can use our API to access Meetupcall API endpoints, which are currently limited to automating the customer sign-up process.

We have language examples in Curl (shell) and Ruby. You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right. The API attempts to follow RESTful principles so using it from other languages shouldn't be a problem.

If you want to try these APIs out in an interactive manner you should use our [Browser Test Harness](https://manage.meetupcall.com/api/v1/docs).

# Authentication

> To authorize, use this code:

```ruby
client = SignupClient.new('pretend_api_key')
```

```shell
# With cURL, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "x-api-key: pretend_api_key"
```

> Make sure to replace `pretend_api_key` with your API key.

Meetupcall uses API keys to allow access to the API. You can request an API key by contacting us via email on the link to the left.

Meetupcall expects for the API key to be included in all API requests to the server in a header that looks like the following:

`x-api-key: pretend_api_key`

<aside class="notice">
You must replace `pretend_api_key` with your personal API key.
</aside>

# Signups

## Get all Signups

```ruby
client = SignupClient.new('pretend_api_key')
client.index
```

```shell
# With curl, this example shows use of the Accept header, which you can modify to return JSON or XML.
curl https://manage.meetupcall.com/api/v1/signups -H "x-api-key: pretend_api_key"  -H "Accept:application/json"
```

> The above command returns JSON structured like this:

```json
[
  {  
     "email":"john.smith@gmail.com",
     "login_url":"http://localhost:3000/login/ACL6LGVJHZc"
  },
  {  
     "email":"johnny.appleseed@gmail.com",
     "login_url":"http://localhost:3000/login/6rXvEY6wVbU"
  },
  {  
     "email":"bob.jones@outlook.com",
     "login_url":"http://localhost:3000/login/MgsrsRZtQeQ"
  },
  {  
     "email":"jane.doe@hotmail.com",
     "login_url":"http://localhost:3000/login/f2AykXcRwuM"
  }
]
```

This endpoint retrieves a collection of the email addresses and login_urls of all Signups previously created through API with your key.

### HTTP Request

`GET https://manage.meetupcall.com/api/v1/signups`

## Get a Specific Signup

```ruby

client = SignupClient.new('pretend_api_key')
client.get('john.smith@gmail.com')
```

```shell
curl https://manage.meetupcall.com/api/v1/signups/john.smith@gmail.com -H "x-api-key: pretend_api_key"  -H "Accept:application/json"
```

> The above command returns JSON structured like this:

```json
{
  "success": true,
  "login_url":"https://manage.meetupcall.com/login/TCL6LGVJHZc"
}
```

This endpoint retrieves a specific Signup.

### HTTP Request

`GET https://manage.meetupcall.com/avpi/v1/<EMAIL>`

### URL Parameters

Parameter | Description
--------- | -----------
EMAIL | The email address of the signup to retrieve

