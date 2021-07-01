# Product Similarity API

## API

* Authorization will be performed via auth-v1-svcs!
* The Shop ID will be persisted along with the Token data, so just pass the api token as a header in all skafos backend requests.
* Staging API requests will hit the base URL: [https://api-staging.skafos.ai](https://api-staging.skafos.ai/)
* Production API requests will hit the base URL:[https://api.skafos.ai](https://api.skafos.ai)</span>

## Headers

All HTTP calls will utilize the following headers:

* Content-Type: application/json
* Authorization: Bearer {JWT api token}

Body

* productID: shopify product ID
* collectionID: shopify collection ID
* count: N (integer)

## Endpoint(s)

See later in doc for error format and table

### **POST /v1/products/similar**

* Fetch the N (defaults to 8) “most similar” products to an input product in a given product collection.
* Example response:

```js
{
    'statusCode': 200,
    'statusMessage': 'OK',
    'statusDescription': 'Request succeeded without error',
    'result': {
        'products': [
            'gid://shopify/Product/152728371252', 
            'gid://shopify/Product/4589734569865',
            …...
        ] 
    }
}
```

## Errors

Example error:

```js
    {
        'statusCode': 401,
        'statusMessage': 'Unauthorized',
        'statusDescription': 'User isn't authorized to access this resource',
        'result': {
            'isValid': false,
            'reason': 'Invalid credentials'
        }
    }

    {
        "statusCode": 400,
        "statusMessage": "Bad Request",
        "statusDescription": "Request is invalid, missing parameters?",
        "result": {
            "reason": "Collection ID not found"
        }
    }

    {
        "statusCode": 400,
        "statusMessage": "Bad Request",
        "statusDescription": "Request is invalid, missing parameters?",
        "result": {
            "reason": "Product ID not found"
        }
    }

    {
        "statusCode": 400,
        "statusMessage": "Bad Request",
        "statusDescription": "Request is invalid, missing parameters?",
        "result": {
            "reason": "Must provide a collectionID"
        }
    }

    {
        "statusCode": 400,
        "statusMessage": "Bad Request",
        "statusDescription": "Request is invalid, missing parameters?",
        "result": {
            "reason": "Must provide a productID"
        }
    }
```

## Future

* Collection ID no longer required.
* Multiple Product ID inputs.
* Body param: “attributes”: [“price”, “title”, “pdp_url”]?
