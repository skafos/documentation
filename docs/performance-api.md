# Performance Dashboard API

## Endpoints

### **Collections**

??? pied-piper "Fetch Collection ID(s)"

    * Fetch the active collection ID(s) for a shop in order to identify the collection ID(s) for use in the rest of the dashboard API requests.

    ```
    POST /v1/collections
    ```
    === "Request"



        ``` json
        {
          "shopID": "gid://shopify/Shop/53276901576",
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
        |shopID* | Shopify Shop ID  |

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
          "shopID": "gid://shopify/Shop/53276901576",
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
        |shopID* | Shopify Shop ID  |
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
                    {"date": "2021-03-01", "likes": 14},
                    {"date": "2021-03-02", "likes": 23}
                ]
            },
            "options": {
                "shopID": "gid://shopify/Shop/53276901576",
                "startDate": "2021-03-16",
                "endDate": "2021-03-29",
                "count": 10
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
          "shopID": "gid://shopify/Shop/53276901576",
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
        |shopID* | Shopify Shop ID  |
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
                    {"date": "2021-03-01", "dislikes": 14},
                    {"date": "2021-03-02", "dislikes": 23}
                ]
            },
            "options": {
                "shopID": "gid://shopify/Shop/53276901576",
                "startDate": "2021-03-16",
                "endDate": "2021-03-29",
                "count": 10
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
          "shopID": "gid://shopify/Shop/53276901576",
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
        |shopID* | Shopify Shop ID  |
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
            },
            "options": {
                "shopID": "gid://shopify/Shop/53276901576",
                "startDate": "2021-03-16",
                "endDate": "2021-03-29",
                "count": 10
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
          "shopID": "gid://shopify/Shop/53276901576",
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
        |shopID* | Shopify Shop ID  |
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
                        "pdpVisits": 35,
                        "rank": 1
                    }, {
                        "id": "gid://shopify/Product/200YLRM05B-V",
                        "product": "Gothamite Ivory Soft Awning Stripes Rug",
                        "imageUrl": "https://www.rug-images.com/products/s/200YLRM05B.jpg",
                        "pdpUrl": "https://www.rugsusa.com/rugsusa/rugs/rugs-usa-soft-awning-stripes/ivory/200YLRM05A-P.html",
                        "pdpVisits": 23,
                        "rank": 2
                    }
                ]
            },
            "options": {
                "shopID": "gid://shopify/Shop/53276901576",
                "startDate": "2021-03-16",
                "endDate": "2021-03-29",
                "count": 10
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
          "shopID": "gid://shopify/Shop/53276901576",
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
        |shopID* | Shopify Shop ID  |
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
                        "pdpVisits": 35,
                        "rank": 1
                    }, {
                        "id": "gid://shopify/Product/200YLRM05B-V",
                        "product": "Gothamite Ivory Soft Awning Stripes Rug",
                        "imageUrl": "https://www.rug-images.com/products/s/200YLRM05B.jpg",
                        "pdpUrl": "https://www.rugsusa.com/rugsusa/rugs/rugs-usa-soft-awning-stripes/ivory/200YLRM05A-P.html",
                        "pdpVisits": 23,
                        "rank": 2
                    }
                ]
            },
            "options": {
                "shopID": "gid://shopify/Shop/53276901576",
                "startDate": "2021-03-16",
                "endDate": "2021-03-29",
                "count": 10
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
          "shopID": "gid://shopify/Shop/53276901576",
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
        |shopID* | Shopify Shop ID  |
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
                        "pdpVisits": 35,
                        "rank": 1
                    }, {
                        "id": "gid://shopify/Product/200YLRM05B-V",
                        "product": "Gothamite Ivory Soft Awning Stripes Rug",
                        "imageUrl": "https://www.rug-images.com/products/s/200YLRM05B.jpg",
                        "pdpUrl": "https://www.rugsusa.com/rugsusa/rugs/rugs-usa-soft-awning-stripes/ivory/200YLRM05A-P.html",
                        "pdpVisits": 23,
                        "rank": 2
                    }
                ]
            },
            "options": {
                "shopID": "gid://shopify/Shop/53276901576",
                "startDate": "2021-03-16",
                "endDate": "2021-03-29",
                "count": 10
            }
        }
        ```

### **Funnel**

??? pied-piper "Fetch Funnel Data"

    The number of pageviews, impressions, sessionsWithInteractions, and pdpVisits by date for a shop or a shop collection over a date range (default is previous 14 days). 

    ```
    POST /v1/performance/funnel
    ```
    === "Request"



        ``` json
        {
          "shopID": "gid://shopify/Shop/53276901576",
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
        |shopID* | Shopify Shop ID  |
        | collectionID  | If not supplied, will aggregate by shop |
        | startDate | Format %Y-%m-%d; if not supplied, will use date 14 days ago |
        | endDate   | If not supplied, will use date 1 day ago |
        | aggregate   | Set to false to request data by date |

    === "Response"

        ```json
        {
            "statusCode": 200,
            "statusMessage": "OK",
            "statusDescription": "Request succeeded without error",
            "result": {
                "funnel": {
                    "pageviews": 1278,
                    "impressions": 846,
                    "sessionsWithInteractions": 267,
                    "pdpVisits": 64
                }
            },
            "options": {
                "shopID": "gid://shopify/Shop/53276901576",
                "startDate": "2021-03-16",
                "endDate": "2021-03-29",
                "aggregate": true
            }
        }
        ```

### **Orders**

??? pied-piper "Fetch Orders"

    The cart/orders information by date for a shop or a shop collection over a date range (default is previous 14 days). 

    ```
    POST /v1/performance/orders
    ```
    === "Request"



        ``` json
        {
          "shopID": "gid://shopify/Shop/53276901576",
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
        |shopID* | Shopify Shop ID  |
        | collectionID  | If not supplied, will aggregate by shop |
        | startDate | Format %Y-%m-%d; if not supplied, will use date 14 days ago |
        | endDate   | If not supplied, will use date 1 day ago |
        | aggregate   | Set to false to request data by date |

    === "Response"

        ```json
        {
            "statusCode": 200,
            "statusMessage": "OK",
            "statusDescription": "Request succeeded without error",
            "result": {
                "orders": {
                    "sessionsWithAddToCart": 25,
                    "averageOrderValue": 129.99,
                    "skafosDrivenRevenue": 1299.90,
                    "totalStoreRevenue": 9999.99,
                    "totalSkafosDrivenRevenue": 99.99
                }
            },
            "options": {
                "shopID": "gid://shopify/Shop/53276901576",
                "startDate": "2021-03-16",
                "endDate": "2021-03-29",
                "aggregate": true
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
