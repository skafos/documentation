# Performance Dashboard API

## Endpoints

### **Authentication**

??? pied-piper "Fetch an API Token"

    Login using a Shopify shopID, shopUrl and long-lived oauth token. The goal of this API endpoint is to allow the shopify dashboard to obtain a JWT access token for use with secure API calls to the Skafos platform.

    ```
    POST /v1/auth/shopifylogin
    ```
    === "Request"



        ``` json
        {
          "shopID": "gid://shopify/Shop/8349675345",
          "shopUrl": "skafos-fashion.myshopify.com",
          "oauth": "shpat_17ddce2eFAKEe6417bce8ab88454387d"
        }
        ```
        ___

        Parameters^*\ Required^ 

        ___

        | Name    | Description                        |
        |---------|------------------------------------|
        | shopID*  | Shopify Shop ID                    |
        | shopUrl* | URL of a Shopify store             |
        | oauth*   | Unencrypted long-lived oAuth token |

    === "Response"

        ``` json
        {
          "statusCode": 200,
          "statusMessage": "OK",
          "statusDescription": "Request succeeded without error",
          "result": {
            "token": "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VySUQiOiJza2Fmb3MtZmFzaGlvbi5teXNob3BpZnkuY29tIiwicGFzc3dvcmQiOiIzMzkzOTUwYzE0YWZjYTAyNmRiNWVkNTM2YjRlMWVmNSIsInJvbGVzIjpbImFwaSJdLCJpc3N1ZXIiOiJ1cm46YXV0aCIsInR5cGUiOiJhY2Nlc3MiLCJpYXQiOjE2MTY4NzE5OTIsImV4cCI6MTYxNjg3NTU5Mn0.gcIR_FJwN0m6JW7ncJSkhI4ZQJv_IbrCwjAUh5FKZBxsitVjP2wbCb1TCMDfVqG7d5zWy_6i20CSnBpfOgUHt2whT0lI6XDSB8hiaLuTez_adnGJdtz-0L6JHbLEHk7GGQKSQgALqXPDjTEqRPZO9L2Wgl7G2yvt6bgqkMKHhV0",
            "refreshToken": "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VySUQiOiJza2Fmb3MtZmFzaGlvbi5teXNob3BpZnkuY29tIiwicGFzc3dvcmQiOiIzMzkzOTUwYzE0YWZjYTAyNmRiNWVkNTM2YjRlMWVmNSIsInJvbGVzIjpbImFwaSJdLCJpc3N1ZXIiOiJ1cm46YXV0aCIsInR5cGUiOiJyZWZyZXNoIiwiaWF0IjoxNjE2ODcxOTkzLCJleHAiOjE2MTkyOTExOTN9.B4JK94WnIEhfRRFC-0NGHKfSkqSbeJSayM29mFTAa3ep9iVCJoWdkLc8QMJI0Xy6C6D38wWKQrcmiBjncIYxSWmBtUOuUf3dYfKNHdeNeQZzAK8NSy4QX6BwfXaP_t4WAD1NVMi_PzB9J4v5Hqgic36GEw7yqyPkbzmrqNal75Y",
            "user": {
              "shopID": "gid://shopify/Shop/8349675345",
              "userID": "skafos-fashion.myshopify.com",
              "roles": [
                "api"
              ],
              "issuer": "urn:auth",
              "type": "refresh",
              "iat": 1616871993,
              "exp": 1619291193
            }
          }
        }
        ```

### **Collections**

??? pied-piper "Fetch Collection ID(s)"

    * Fetch the active collection ID(s) for a shop in order to identify the collection ID(s) for use in the rest of the dashboard API requests
    * To get the names to display in the dropdown, use the collection IDs from the response to retrieve the collection titles (by ID) from Shopify via GraphQL (or REST) API - NOTE THAT THIS WILL BE THE RESPONSIBILITY OF THE DASHBOARD SERVICE

    ```
    POST /v1/collections
    ```
    === "Request"



        ``` json
        {

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
        |shop_id* | Shopify Shop ID  |

    === "Response"

        ```json
        {
            "statusCode": 200,
            "statusMessage": "OK",
            "statusDescription": "Request succeeded without error",
            "result": {
                "shopID": "gid://shopify/Shop/53276901576",
                "collections": [
                    "gid://shopify/Collection/242584846536"
                ]
            }
        }
        ```

### **Likes**

??? pied-piper "Fetch Likes"

    The number of likes by date for a shop or a shop collection over a date range (default is previous 14 days).

    ```
    POST /v1/performance/likes
    ```
    === "Request"



        ``` json
        {

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
        |shop_id* | Shopify Shop ID  |
        | collectionID  | If not supplied, will aggregate by shop |
        | startDate | Format %Y-%m-%d; if not supplied, will use date 14 days ago |
        | endDate   | If not supplied, will use date 1 day ago |

    === "Response"

        ```json
          {
              "statusCode": 200,
              "statusMessage": "OK",
              "statusDescription": "Request succeeded without error",
              "result": {
              "likes": [
                {"date": "2021-03-01", "likes": 54},
                {"date": "2021-03-02", "likes": 72}
                ]
              }
          }
        ```

### **Dislikes**

??? pied-piper "Fetch Dislikes"

    The number of dislikes by date for a shop or a shop collection over a date range (default is previous 14 days).

    ```
    POST /v1/performance/dislikes
    ```
    === "Request"



        ``` json
        {

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
        |shop_id* | Shopify Shop ID  |
        | collectionID  | If not supplied, will aggregate by shop |
        | startDate | Format %Y-%m-%d; if not supplied, will use date 14 days ago |
        | endDate   | If not supplied, will use date 1 day ago |

    === "Response"

        ```json
        {
            "statusCode": 200,
            "statusMessage": "OK",
            "statusDescription": "Request succeeded without error",
            "result": {
            "dislikes": [
              {"date": "2021-03-01", "dislikes": 23},
              {"date": "2021-03-02", "dislikes": 89}
              ]
            }
        }
        ```

### **PDP Visits**

??? pied-piper "Fetch PDP Visits"

    The number of PDP visits by date for a shop or a shop collection over a date range (default is previous 14 days).

    ```
    POST /v1/performance/pdp_visits
    ```
    === "Request"



        ``` json
        {

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
        |shop_id* | Shopify Shop ID  |
        | collectionID  | If not supplied, will aggregate by shop |
        | startDate | Format %Y-%m-%d; if not supplied, will use date 14 days ago |
        | endDate   | If not supplied, will use date 1 day ago |

    === "Response"

        ```json
        {
            "statusCode": 200,
            "statusMessage": "OK",
            "statusDescription": "Request succeeded without error",
            "result": {
            "pdpVisits": [
              {"date": "2021-03-01", "pdpVisits": 14},
              {"date": "2021-03-02", "pdpVisits": 23}
              ]
            }
        }
        ```

### **Top Likes**

??? pied-piper "Fetch Top Likes"

    The ranked products (default count is 10) by likes for a shop or a shop collection over a date range (default is previous 14 days), includes id, product (name), imageUrl, pdpUrl, likes (count), and rank.

    ```
    POST /v1/performance/top_likes
    ```
    === "Request"



        ``` json
        {

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
        |shop_id* | Shopify Shop ID  |
        | collectionID  | If not supplied, will aggregate by shop |
        | startDate | Format %Y-%m-%d; if not supplied, will use date 14 days ago |
        | endDate   | If not supplied, will use date 1 day ago |
        | count   | For top product requests only; if not supplied, will provide top 10 products |

    === "Response"

        ```json
        {
            "statusCode": 200,
            "statusMessage": "OK",
            "statusDescription": "Request succeeded without error",
            "result": {
              "topLikes": [
                  {
                        "id": "gid://shopify/Product/200MTVS176A-V", 
                        "product": "Tuscan Baby Blue Dotted Diamond Trellis Nursery Rug", 
                        "imageUrl": "https://www.rug-images.com/products/s/200MTVS176A.jpg", 
                        "pdpUrl": "https://www.rugsusa.com/rugsusa/rugs/rugs-usa-dotted-diamond-trellis-nursery/baby-blue/200MTVS176A-P.html", 
                        "likes": 94,
                            "rank": 1
                      },
                  {
                      "id": "gid://shopify/Product/200YLRM05B-V", 
                      "product": "Gothamite Ivory Soft Awning Stripes Rug", 
                      "imageUrl": "https://www.rug-images.com/products/s/200YLRM05B.jpg", 
                      "pdpUrl": "https://www.rugsusa.com/rugsusa/rugs/rugs-usa-soft-awning-stripes/ivory/200YLRM05A-P.html", 
                      "likes": 87,
                            "rank": 2
                  }
                ]
            }
        }
        ```

### **Top Dislikes**

??? pied-piper "Fetch Top Disikes"

    The ranked products (default count is 10) by dislikes for a shop or a shop collection over a date range (default is previous 14 days), includes id, product (name), imageUrl, pdpUrl, dislikes (count), and rank.

    ```
    POST /v1/performance/top_dislikes
    ```
    === "Request"



        ``` json
        {

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
        |shop_id* | Shopify Shop ID  |
        | collectionID  | If not supplied, will aggregate by shop |
        | startDate | Format %Y-%m-%d; if not supplied, will use date 14 days ago |
        | endDate   | If not supplied, will use date 1 day ago |
        | count   | For top product requests only; if not supplied, will provide top 10 products |

    === "Response"

        ```json
        {
            "statusCode": 200,
            "statusMessage": "OK",
            "statusDescription": "Request succeeded without error",
            "result": {
              "topDislikes": [
                  {
                        "id": "gid://shopify/Product/200MTVS176A-V", 
                        "product": "Tuscan Baby Blue Dotted Diamond Trellis Nursery Rug", 
                        "imageUrl": "https://www.rug-images.com/products/s/200MTVS176A.jpg", 
                        "pdpUrl": "https://www.rugsusa.com/rugsusa/rugs/rugs-usa-dotted-diamond-trellis-nursery/baby-blue/200MTVS176A-P.html", 
                        "dislikes": 35,
                            "rank": 1
                      },
                  {
                      "id": "gid://shopify/Product/200YLRM05B-V", 
                      "product": "Gothamite Ivory Soft Awning Stripes Rug", 
                      "imageUrl": "https://www.rug-images.com/products/s/200YLRM05B.jpg", 
                      "pdpUrl": "https://www.rugsusa.com/rugsusa/rugs/rugs-usa-soft-awning-stripes/ivory/200YLRM05A-P.html", 
                      "dislikes": 23,
                            "rank": 2
                  }
                ]
            }
        }
        ```

### **Top PDP Visits**

??? pied-piper "Fetch Top PDP Visits"

    The ranked products (default count is 10) by PDP visits for a shop or a shop collection over a date range (default is previous 14 days), includes id, product (name), imageUrl, pdpUrl, pdpVisits (count), and rank.

    ```
    POST /v1/performance/top_pdp_visits
    ```
    === "Request"



        ``` json
        {

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
        |shop_id* | Shopify Shop ID  |
        | collectionID  | If not supplied, will aggregate by shop |
        | startDate | Format %Y-%m-%d; if not supplied, will use date 14 days ago |
        | endDate   | If not supplied, will use date 1 day ago |
        | count   | For top product requests only; if not supplied, will provide top 10 products |

    === "Response"

        ```json
        {
            "statusCode": 200,
            "statusMessage": "OK",
            "statusDescription": "Request succeeded without error",
            "result": {
              "topPdpVisits": [
                  {
                        "id": "gid://shopify/Product/200MTVS176A-V", 
                        "product": "Tuscan Baby Blue Dotted Diamond Trellis Nursery Rug", 
                        "imageUrl": "https://www.rug-images.com/products/s/200MTVS176A.jpg", 
                        "pdpUrl": "https://www.rugsusa.com/rugsusa/rugs/rugs-usa-dotted-diamond-trellis-nursery/baby-blue/200MTVS176A-P.html", 
                        "pdpVisits": 23,
                            "rank": 1
                      },
                  {
                      "id": "gid://shopify/Product/200YLRM05B-V", 
                      "product": "Gothamite Ivory Soft Awning Stripes Rug", 
                      "imageUrl": "https://www.rug-images.com/products/s/200YLRM05B.jpg", 
                      "pdpUrl": "https://www.rugsusa.com/rugsusa/rugs/rugs-usa-soft-awning-stripes/ivory/200YLRM05A-P.html", 
                      "pdpVisits": 19,
                            "rank": 2
                  }
                ]
            }
        }
        ```

## Errors

Example errors:

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
      "reason": "Collections not found for shop gid://shopify/Shop/thingy"
  }
}
```

| statusCode | statusDescription                             |
|------------|-----------------------------------------------|
| 400        | Request is invalid, missing parameters        |
| 401        | User isn"t authorized to access this resource |
| 500        | Internal service error: {“error”:}            |
| 503        | Service Unavailable                           |
