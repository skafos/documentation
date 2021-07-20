# Product Similarity API

## Endpoint

### **Similar Products**

??? pied-piper "Fetch Similar Products"

    Fetch the N (defaults to 8) “most similar” products to an input product in a given product collection.

    ```
    POST /v1/products/similar
    ```
    === "Request"



        ``` json
        {
          "productID": "gid://shopify/Product/197578471252",
          "collectionID": "gid://shopify/Collection/242584846536",
          "count": "10"
        }
        ```
        ___

        Headers

        ___

        | Headers       |                        |
        |---------------|------------------------|
        | Content-Type  | application/json       |
        | Authorization | Bearer \{JWT api token\} |

        ___


        Parameters^*\ Required^ 

        ___

        | Name    | Description                        |
        |---------|------------------------------------|
        | productID*  | shopify product ID |
        | collectionID* | shopify collection ID |
        | count   | N (integer) |

    === "Response"

        ``` json
            {
                "statusCode": 200,
                "statusMessage": "OK",
                "statusDescription": "Request succeeded without error",
                "result": {
                    "products": [
                        "gid://shopify/Product/152728371252", 
                        "gid://shopify/Product/9545794737943",
                        "gid://shopify/Product/4324854837844",
                        "gid://shopify/Product/4598738748734",
                        "gid://shopify/Product/1857498373347",
                        "gid://shopify/Product/6583953405934",
                        "gid://shopify/Product/32903594785420",
                        "gid://shopify/Product/40593859340322",
                        "gid://shopify/Product/5897345694865",
                        "gid://shopify/Product/7643983497839",
                        
                    ] 
                }
            }
        ```

## Errors

Example error:

```json
    {
        "statusCode": 401,
        "statusMessage": "Unauthorized",
        "statusDescription": "User isn't authorized to access this resource",
        "result": {
            "isValid": false,
            "reason": "Invalid credentials"
        }
    }
```

```json
    {
        "statusCode": 400,
        "statusMessage": "Bad Request",
        "statusDescription": "Request is invalid, missing parameters?",
        "result": {
            "reason": "Collection ID not found"
        }
    }
```

```json
    {
        "statusCode": 400,
        "statusMessage": "Bad Request",
        "statusDescription": "Request is invalid, missing parameters?",
        "result": {
            "reason": "Product ID not found"
        }
    }
```

```json
    {
        "statusCode": 400,
        "statusMessage": "Bad Request",
        "statusDescription": "Request is invalid, missing parameters?",
        "result": {
            "reason": "Must provide a collectionID"
        }
    }
```

```json
    {
        "statusCode": 400,
        "statusMessage": "Bad Request",
        "statusDescription": "Request is invalid, missing parameters?",
        "result": {
            "reason": "Must provide a productID"
        }
    }
```