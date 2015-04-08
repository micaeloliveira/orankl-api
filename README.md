orankl-api
==========

To gain API access to Orankl.com, please contact support@orankl.com

## Review integration

You will need to add the following script to the head of your pages, with your store key

````html
<script src="https://www.orankl.com/javascript?store_key=your-store-key-here" type="text/javascript"></script>
````

As well as the following snippet on each one of your product pages, with the corresponding values replaced

````html
<div id="orankl-reviews"
  data-store-key="YOUR STORE KEY"
  data-product-name="PRODUCT NAME"
  data-product-key="UNIQUE PRODUCT IDENTIFIER"
  data-product-image-url="PRODUCT IMAGE URL"
  data-product-description="PRODUCT DESCRIPTION"
  data-product-price="PRODUCT PRICE"
  data-currency="PRODUCT CURRENCY"
></div>
````

## review_request

The review_request enpoint is used to send "review request notifications" to customers after they have made a purchase. This sends them an email prompting them to leave a review for the product(s) they purchased. The email is sent after the number of days you have configured in the orankl dashboard.

Make a post to this endpoint with customer and order information after the order has been fulfilled to trigger the email.

#### Location

Method  | Endpoint
------------- | -------------
POST  | `https://www.orankl.com/api/review_request`


#### Authorization

Each request will need an authorization header including your secret access token

`Authorization: Token token=your-secret-access-token-here`

#### Prameters

The following params are available to send via JSON

Key  | Value | Required
------------- | ------------- | -------------
`store_key`  | your unique store key (ex: `27cea66f-d942-47d3-b1e8-ab4258152828`) | required
`order:order_id`  | a unique identifier for the given order (this could be a database id) | required
`customer:name` | name of customer who made purchase | required
`customer:email` | email of customer who made purchase | required
`customer:birthdate` | email of customer who made purchase | optional
`customer:gender` | email of customer who made purchase | optional
`product:key` | a unique identifier for the purchased product (this could be a database id) | required
`product:name` | name of product | required
`product:url` | url of product | optional (recommended)
`product:image` | image url of product | optional (recommended)
`product:description` | description of product | optional (recommended)
`product:price` | price of product | required
`product:currency` | currency of product | required

#### Example Format

````json
{
  "store_key":"27cea66f-d942-47d3-b1e8-ab4258152828",
  "order":{
    "order_id":"#123",
    "customer":{
      "email":"mica+apitest@orankl.com",
      "name":"Micael Oliveira"
    },
    "products":[
      {
        "key":"1",
        "name":"product 1",
        "url":"http://store.com/product_1",
        "image":"http://store.com/product_image.jpg",
        "description":"Product description",
        "price":"1.99",
        "currency":"USD"
      }
    ]
  }
}
````

#### Example curl request

````bash
curl https://www.orankl.com/api/review_request \
  -X POST \
  -H "Content-Type: application/json" \ 
  -H "Authorization: Token token=74459d337947c1f170519fbbe38ef56c" \
  -d '{ "store_key":"27cea66f-d942-47d3-b1e8-ab4258152828", "order":{ "order_id":"#123", "customer":{ "email":"mica+apitest@orankl.com", "name":"Micael Oliveira" }, "products":[ { "key":"1", "name":"product 1", "url":"http://store.com/product_1", "image":"http://store.com/images/product_1.jpg", "description":"Product description", "price":"1.99", "currency":"USD" } ] } }' 
````
