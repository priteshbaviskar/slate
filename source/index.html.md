---
title: Storeplum - API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - javascript
  - java

toc_footers:
  - <a href='https://storeplum.in'>Copyright © 2022 Storeplum</a>

includes:
  - errors

search: true

code_clipboard: true

meta:
  - name: Storeplum - API Reference
    content: Storeplum API documentation for external integrations.
---

# Overview

The purpose of this documentation is to understand the list of available Storeplum APIs and their corresponding requests and response for a seamless Zapier integration of Storeplum with your app. Storeplum API 1.0 allows data to be created, read and updated using requests in JSON format and using standard REST HTTP methods which are understood by most of the HTTP clients.

The current Storeplum REST API integration version is `v1` which takes a first-order position in endpoints. 

We have language bindings in Shell, Java and JavaScript. You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

## Request/Response Format

The default response format is JSON. Requests with a message-body use plain JSON to set or update resource attributes. Successful requests will return a `200 OK HTTP` status.

Some general information about responses:

1. Resource IDs are returned as integers.
2. Any decimal monetary amount, such as prices or totals, will be returned as strings with two decimal places. 
3. Other amounts, such as item counts, are returned as integers. 
4. Blank fields are generally included as null or emtpy string instead of being omitted.




# Authentication

Each incoming request from Zapier to Storeplum API has to be authenticated using pre-generated keys. Storeplum uses pre-generated API keys for Zapier integration which can be obtained in [Storeplum Dashboard](https://dashboard.storeplum.in/) under integrations section. 

Click on Zapier to activate your Zapier integration with Storeplum. Once activated, copy the API key seen on the screen. Please make sure to save this key as it won't be available to view later.


![Activating Zapier integration for Storeplum](images/image-zapier.png)


> To authorize, use this code:


```java
import okhttp3.*;

Request request = new Request.Builder()
                .url(url)
                .post(body)
                .addHeader("X-SP-INTEGRATION", <YOUR-API-KEY>)
                .build();
Response response = okHttpClient.newCall(request).execute();
```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here" \
  -H "X-SP-INTEGRATION: <YOUR-API-KEY>"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
```

> Make sure to replace `x-sp-integration` with your API key.

Storeplum uses the above API key to allow access to the APIs. Include this API key in all requests to Storeplum API in a header with name `X-SP-INTEGRATION`

`X-SP-INTEGRATION: <YOUR-API-KEY>`

<aside class="notice">
You must replace <code>YOUR-API-KEY</code> with your personal API key.
</aside>

# Storeplum Events

## Subscribe to New Customer Event

Add your webhook url to start listening to new customer event. This event is triggered whenever a new customer is added to your Storeplum account.

```java
import okhttp3.*;

Map<String, Object> data = new HashMap<>();
data.put("hookUrl", "<your-webhook-url>");
data.put("customerCode", "your-storeplum-customer-code");

RequestBody body = RequestBody.create(new Gson().toJson(data),
                MediaType.parse("application/json"));

Request request = new Request.Builder()
                .url("https://api.storeplum.in/giclee-admin-service/admin/integration/zapier/new_customer/subscribe")
                .post(body)
                .addHeader("X-SP-INTEGRATION", <YOUR-API-KEY>)
                .build();
Response response = okHttpClient.newCall(request).execute();
```

```shell
curl "https://api.storeplum.in/giclee-admin-service/admin/integration/zapier/new_customer/subscribe" \
  -H "X-SP-INTEGRATION: <YOUR-API-KEY>"\
  -d '{
    hookUrl: "<your-webhook-url>",
    customerCode: "your-storeplum-customer-code"
  }'
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let kittens = api.kittens.get();
```

> Success Response `200 OK`

```json
{
  "isSuccess": true,
  "message": "success",
  "object": {
    "uniqueID" : "subscription-id-for-this-webhook"
  }
}
```
> Success Response `400 BAD REQUEST`

```json
{
  "isSuccess": false,
  "message": "invalid_input",
  "object": {}
  
}
```

### HTTP Request

`POST https://api.storeplum.in/giclee-admin-service/admin/integration/zapier/new_customer/subscribe`

### Body Parameters

Parameter | Description
--------- | -----------
hookUrl | Your webhook url where you'd like to listen for this event.
customerCode | Storeplum Customer Code which can be found in your Storeplum Dashboard.

## Subscribe to Add New Product Event

Add your webhook url to start listening to add new product event. This event is triggered whenever a new product is added to your Storeplum account.

```java
import okhttp3.*;

Map<String, Object> data = new HashMap<>();
data.put("hookUrl", "<your-webhook-url>");
data.put("customerCode", "your-storeplum-customer-code");

RequestBody body = RequestBody.create(new Gson().toJson(data),
                MediaType.parse("application/json"));

Request request = new Request.Builder()
                .url("https://api.storeplum.in/giclee-admin-service/admin/integration/zapier/new_product/subscribe")
                .post(body)
                .addHeader("X-SP-INTEGRATION", <YOUR-API-KEY>)
                .build();
Response response = okHttpClient.newCall(request).execute();
```

```shell
curl "https://api.storeplum.in/giclee-admin-service/admin/integration/zapier/new_product/subscribe" \
  -H "X-SP-INTEGRATION: <YOUR-API-KEY>"\
  -d '{
    hookUrl: "<your-webhook-url>",
    customerCode: "your-storeplum-customer-code"
  }'
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let kittens = api.kittens.get();
```

> Success Response `200 OK`

```json
{
  "isSuccess": true,
  "message": "success",
  "object": {
    "uniqueID" : "subscription-id-for-this-webhook"
  }
}
```

### HTTP Request

`POST https://api.storeplum.in/giclee-admin-service/admin/integration/zapier/new_product/subscribe`

### Body Parameters

Parameter | Description
--------- | -----------
hookUrl | Your webhook url where you'd like to listen for this event.
customerCode | Storeplum Customer Code which can be found in your Storeplum Dashboard.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>


## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```java
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2" \
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

## Delete a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.delete(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.delete(2)
```

```shell
curl "http://example.com/api/kittens/2" \
  -X DELETE \
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete

