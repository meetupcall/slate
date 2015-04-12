---
title: API Reference

language_tabs:
  - shell
  - ruby
  - csharp

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

```csharp

// C#, VB.NET or other .NET clients can use our client library available at https://github.com/meetupcall/meetupcall-api-dotnet

```

Welcome to alpha version Meetupcall V1 API. You can use our API to access Meetupcall API endpoints, which are currently limited to automating the customer sign-up process.

We have language examples in Curl (shell) and Ruby. You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right. The API attempts to follow RESTful principles so using it from other languages shouldn't be a problem.

If you want to try these APIs out in an interactive manner you should use our [Browser Test Harness](https://manage.meetupcall.com/api/v1/docs).

# Authentication

> To authenticate, use this code:

```csharp
var client = new SignupClient("pretend_api_key");
```

```ruby
client = SignupClient.new('pretend_api_key')
```

```shell
# With Curl, you can just pass the correct header with each request
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

## Create a Signup

```csharp
var request = new SignupRequest {
  email = "john.smith@gmail.com",
  first_name = "John",
  last_name = "Smith",
  account_name = "Acme Corp",
  billing_street = "29 Acacia Road",
  billing_city = "London",
  billing_postal_code = "SW19 5AG",
  billing_country = "GB"
};

var new_signup = client.Create(request);
```

```ruby
client = SignupClient.new('pretend_api_key')

client.create({
  email: 'john.smith@gmail.com',
  first_name: 'John',
  last_name: 'Smith',
  account_name: 'ACME Corp',
  billing_street: '29 Acacia Road',
  billing_city: 'London',
  billing_postal_code: 'SW19 5AG',
  billing_country: 'GB'}
```

```shell
curl --data '{"email" : "john.smith@gmail.com", "first_name" : "John", "last_name" : "Smith", "account_name" : "ACME Corp", "billing_street" : "29 Acacia Road", "billing_city" : "London", "billing_postal_code" : "SW19 5AG", "billing_country":"GB"}' https://manage.meetupcall.com/api/v1/signups --header "x-api-key: pretend_api_key"  --header "Accept:application/json" --header "Content-Type:application/json"
```

> The above command returns JSON structured like this:

```json
{
  "status": {
    "code": 200,
    "description": "Success."
  },
  "data": {
    "email": "john.smith@gmail.com",
    "login_url": "https://manage.meetupcall.com/login/g45G3fLe-to"
  }
}
```

This endpoint automates the entire Meetupcall signup process and upon success returns a `login_url` you can use to authenticate and log into Meetupcall without entering a password.

It will also send the new User a 'Welcome Email' asking them to activate their account and choose a new password.

### HTTP Request

`POST https://manage.meetupcall.com/api/v1/signups`

### Body Parameters

Parameter | Required?   | Notes
--------- | ----------- | -----
email | Yes
first_name | Yes |
last_name  | Yes |
account_name | Yes |
billing_street | Yes |
billing_city | Yes |
billing_postal_code | Yes |
billing_country | Yes |
phone | No |
billing_state | No |
timezone | No | Default: London

## Get all Signups

```csharp
client = SignupClient.new("pretend_api_key")
client.Index();
```

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
{
  "status": {
    "code": 200,
    "description": "Success."
  },
  "data": [
    {
      "email": "john.smith@gmail.com",
      "login_url": "https://manage.meetupcall.com/login/j9SHCvwBfRk"
    },
    {
      "email": "johnny.appleseed@outlook.com",
      "login_url": "https://manage.meetupcall.com/login/YYEyH8TL2v8"
    },
    {
      "email": "jane.doe@hotmail.com",
      "login_url": "https://manage.meetupcall.com/login/aQS0Wmegmqs"
    }
  ]
}
```

This endpoint retrieves a collection of the email addresses and login_urls of all Signups previously created through the API with your key.

### HTTP Request

`GET https://manage.meetupcall.com/api/v1/signups`

## Get a Specific Signup

```csharp
client = SignupClient.new("pretend_api_key")
client.Get("john.smith@gmail.com");
```

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
  "status": {
    "code": 200,
    "description": "Success."
  },
  "data": {
    "email": "john.smith@gmail.com",
    "login_url": "https://manage.meetupcall.com/login/A45G3cLe-to"
  }
}
```

This endpoint retrieves a specific Signup previously created through the API with your key.

### HTTP Request

`GET https://manage.meetupcall.com/avpi/v1/signups/<email>`

### URL Parameters

Parameter | Required? |Notes
--------- | --------- |-----
email | Yes |The email address of the signup to retrieve

