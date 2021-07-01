# Performance Dashboard API

## API

* auth-v1-svcs and shopify-oauth-v1-svcs are now updated and ready to support shopify dashboard login to retrieve a valid JWT api token.
* Staging API requests will hit the base URL: [https://api-staging.skafos.ai](https://api-staging.skafos.ai/)
* Production API requests will hit the base URL: [https://api.skafos.ai](https://api.skafos.ai)

## Headers

All HTTP calls will utilize the following headers:

* Content-Type: application/json
* Authorization: Bearer {JWT api token}

Naming conventions for params in body:

* collectionID - optional; if not provided, then data will be aggregated across all collections for the shop
* startDate (optional)
* endDate (optional)
* count (optional)

## README

See [https://github.com/skafos/performance-v1-svcs](https://github.com/skafos/performance-v1-svcs) for performance-v1-svcs backend

## Endpoints

See later in doc for error format and table

### **POST [/v1/auth/shopifylogin](https://github.com/skafos/auth-v1-svcs/blob/main/documentation/api-shopifylogin-v1.md)**

* Fetch a JWT api token for the dashboard client
* Body needs to include:
  * shopID - shop ID for the store on which the dashboard appears
  * shopUrl - shopify URL for the store (e.g., skafos-fashion-mini-public.myshopify.com)
  * oauth - valid Shopify offline oAuth token

### **POST /v1/collections**

* Fetch the active collection ID(s) for a shop in order to identify the collection ID(s) for use in the rest of the dashboard API requests
* To get the names to display in the dropdown, use the collection IDs from the response to retrieve the collection titles (by ID) from Shopify via GraphQL (or REST) API - NOTE THAT THIS WILL BE THE RESPONSIBILITY OF THE DASHBOARD SERVICE
* Header needs to include:
  * Authorization - Bearer &lt;active JWT token>
  * Example response:

```js
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

### **POST /v1/performance/likes**

* Count of all likes by date for previous 14 days
* If no collection ID is provided in the header, response will include data aggregated across all collections
* Header needs to include:
  * Authorization - Bearer &lt;active JWT token>
* Optional fields for Body:
  * collectionID
  * startDate
  * endDate
  * Example response:

```js
  {
      'statusCode': 200,
      'statusMessage': 'OK',
      'statusDescription': 'Request succeeded without error',
      'result': {
      'likes': [
        {'date': '2021-03-01', 'likes': 54},
        {'date': '2021-03-02', 'likes': 72}
        ]
      }
  }
```

### **POST** **/v1/performance/dislikes**

* Count of all dislikes by date for previous 14 days
* If no collection ID is provided in the header, response will include data aggregated across all collections
* Header needs to include:
  * Authorization - Bearer &lt;active JWT token>
* Optional fields for Body:
  * collectionID
  * startDate
  * endDate

```js
{
    'statusCode': 200,
    'statusMessage': 'OK',
    'statusDescription': 'Request succeeded without error',
    'result': {
    'dislikes': [
      {'date': '2021-03-01', 'dislikes': 23},
      {'date': '2021-03-02', 'dislikes': 89}
      ]
    }
}
```

### **POST /v1/performance/pdp_visits**

* Count of all PDP visits by date for previous 14 days
* If no collection ID is provided in the header, response will include data aggregated across all collections
* Header needs to include:
  * Authorization - Bearer &lt;active JWT token>
* Optional fields for Body:
  * collectionID
  * startDate
  * endDate

```js
{
    'statusCode': 200,
    'statusMessage': 'OK',
    'statusDescription': 'Request succeeded without error',
    'result': {
    'pdpVisits': [
      {'date': '2021-03-01', 'pdpVisits': 14},
      {'date': '2021-03-02', 'pdpVisits': 23}
      ]
    }
}
```

### **POST /v1/performance/top_likes**

* Top 10 liked products for previous 14 days, including:
  * id
  * product
  * imageUrl
  * pdpUrl
  * likes
  * rank
* If no collection ID is provided in the header, response will include data aggregated across all collections
* Header needs to include:
  * Authorization - Bearer &lt;active JWT token>
* Optional fields for Body:
  * collectionID
  * startDate
  * endDate
  * count
* Example response:

```js
{
    'statusCode': 200,
    'statusMessage': 'OK',
    'statusDescription': 'Request succeeded without error',
    'result': {
      'topLikes': [
          {
                'id': 'gid://shopify/Product/200MTVS176A-V', 
                'product': 'Tuscan Baby Blue Dotted Diamond Trellis Nursery Rug', 
                'imageUrl': 'https://www.rug-images.com/products/s/200MTVS176A.jpg', 
                'pdpUrl': 'https://www.rugsusa.com/rugsusa/rugs/rugs-usa-dotted-diamond-trellis-nursery/baby-blue/200MTVS176A-P.html', 
                'likes': 94,
                    'rank': 1
              },
          {
              'id': 'gid://shopify/Product/200YLRM05B-V', 
              'product': 'Gothamite Ivory Soft Awning Stripes Rug', 
              'imageUrl': 'https://www.rug-images.com/products/s/200YLRM05B.jpg', 
              'pdpUrl': 'https://www.rugsusa.com/rugsusa/rugs/rugs-usa-soft-awning-stripes/ivory/200YLRM05A-P.html', 
              'likes': 87,
                    'rank': 2
          }
        ]
    }
}
```

### **POST /v1/performance/top_dislikes**

* Top 10 disliked products for previous 14 days, including:
  * id
  * product
  * imageUrl
  * pdpUrl
  * dislikes
  * rank
* If no collection ID is provided in the header, response will include data aggregated across all collections
* Header needs to include:
  * Authorization - Bearer &lt;active JWT token>
* Optional fields for Body:
  * collectionID
  * startDate
  * endDate
  * count

```js
{
    'statusCode': 200,
    'statusMessage': 'OK',
    'statusDescription': 'Request succeeded without error',
    'result': {
      'topDislikes': [
          {
                'id': 'gid://shopify/Product/200MTVS176A-V', 
                'product': 'Tuscan Baby Blue Dotted Diamond Trellis Nursery Rug', 
                'imageUrl': 'https://www.rug-images.com/products/s/200MTVS176A.jpg', 
                'pdpUrl': 'https://www.rugsusa.com/rugsusa/rugs/rugs-usa-dotted-diamond-trellis-nursery/baby-blue/200MTVS176A-P.html', 
                'dislikes': 35,
                    'rank': 1
              },
          {
              'id': 'gid://shopify/Product/200YLRM05B-V', 
              'product': 'Gothamite Ivory Soft Awning Stripes Rug', 
              'imageUrl': 'https://www.rug-images.com/products/s/200YLRM05B.jpg', 
              'pdpUrl': 'https://www.rugsusa.com/rugsusa/rugs/rugs-usa-soft-awning-stripes/ivory/200YLRM05A-P.html', 
              'dislikes': 23,
                    'rank': 2
          }
        ]
    }
}
```

### **POST /v1/performance/top_pdp_visits**

* Top 10 products PDP visits for previous 14 days, including:
  * id
  * product
  * imageUrl
  * pdpUrl
  * pdpVisits
  * rank
* If no collection ID is provided in the header, response will include data aggregated across all collections
* Header needs to include:
  * Authorization - Bearer &lt;active JWT token>
* Optional fields for Body:
  * collectionID
  * startDate
  * endDate
  * count

```js
{
    'statusCode': 200,
    'statusMessage': 'OK',
    'statusDescription': 'Request succeeded without error',
    'result': {
      'topPdpVisits': [
          {
                'id': 'gid://shopify/Product/200MTVS176A-V', 
                'product': 'Tuscan Baby Blue Dotted Diamond Trellis Nursery Rug', 
                'imageUrl': 'https://www.rug-images.com/products/s/200MTVS176A.jpg', 
                'pdpUrl': 'https://www.rugsusa.com/rugsusa/rugs/rugs-usa-dotted-diamond-trellis-nursery/baby-blue/200MTVS176A-P.html', 
                'pdpVisits': 23,
                    'rank': 1
              },
          {
              'id': 'gid://shopify/Product/200YLRM05B-V', 
              'product': 'Gothamite Ivory Soft Awning Stripes Rug', 
              'imageUrl': 'https://www.rug-images.com/products/s/200YLRM05B.jpg', 
              'pdpUrl': 'https://www.rugsusa.com/rugsusa/rugs/rugs-usa-soft-awning-stripes/ivory/200YLRM05A-P.html', 
              'pdpVisits': 19,
                    'rank': 2
          }
        ]
    }
}
```

## Errors

Example errors:

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
       "reason": "Collections not found for shop gid://shopify/Shop/thingy"
   }
}
```

| statusCode | statusDescription                             |
|------------|-----------------------------------------------|
| 400        | Request is invalid, missing parameters        |
| 401        | User isn't authorized to access this resource |
| 500        | Internal service error: {“error”:}            |
| 503        | Service Unavailable                           |

## Backend design

See [https://app.diagrams.net/#G1L5LzLcSIR4ecFGfIsh4p07mZyOiN_RPQ](https://app.diagrams.net/#G1L5LzLcSIR4ecFGfIsh4p07mZyOiN_RPQ)

### **/v1/collections**

Sample request:

```js
{
  "to": "shopify-setup-v1-svcs:/",
  "frm": "skafos-api-v1-svcs:/",
  "mid": "9ba5365b-d652-4de0-b3ac-5954cc2fbdf1",
  "typ": "shopify_setup.get_shop_collections",
  "bdy": {
      "shop_id": "gid://shopify/Shop/50975277226"
  }
}
```

Sample response:

```js
{
  "to": "skafos-api-v1-svcs:/",
  "frm": "shopify-setup-v1-svcs:/",
  "rmid": "9ba5365b-d652-4de0-b3ac-5954cc2fbdf1",
  "typ": "shopify_setup.collections",
  "bdy": {
      "shop_id": "gid://shopify/Shop/50975277226",
      "collection_ids": ["gid://shopify/Collection/235800101034"]
  }
}
```

### **/v1/performance/likes**

Sample request:

```js
{
  "to": "performance-v1-svcs:/",
  "frm": "skafos-api-v1-svcs:/",
  "mid": "9ba5365b-d652-4de0-b3ac-5954cc2fbdf1",
  "typ": "performance.likes",
  "bdy": {
      "shop_id": "gid://shopify/Shop/50975277226",
      "collection_id": "gid://shopify/Collection/235800101034"



  } 
} 
```

Sample response:

```js
{
  "to": "skafos-api-v1-svcs:/",
  "frm": "performance-v1-svcs:/",
  "rmid": "9ba5365b-d652-4de0-b3ac-5954cc2fbdf1",
  "typ": "performance.likes",
  "bdy": {
     "likes": [
          {"date": "2021-03-16", "likes": 1},
          {"date": "2021-03-17", "likes": 2}
       ]
  }
}
```

### **/v1/performance/dislikes**

Sample request:

```js
{
  "to": "performance-v1-svcs:/",
  "frm": "skafos-api-v1-svcs:/",
  "mid": "9ba5365b-d652-4de0-b3ac-5954cc2fbdf1",
  "typ": "performance.dislikes",
  "bdy": {
      "shop_id": "gid://shopify/Shop/50975277226",
      "collection_id": "gid://shopify/Collection/235800101034"
  } 
} 
```

Sample response:

```js
{
  "to": "skafos-api-v1-svcs:/",
  "frm": "performance-v1-svcs:/",
  "rmid": "9ba5365b-d652-4de0-b3ac-5954cc2fbdf1",
  "typ": "performance.dislikes",
  "bdy": {
     "dislikes": [
          {"date": "2021-03-16", "dislikes": 1},
          {"date": "2021-03-17", "dislikes": 2}
       ]
  }
}
```

### **/v1/performance/pdp_visits**

Sample request:

```js
{
  "to": "performance-v1-svcs:/",
  "frm": "skafos-api-v1-svcs:/",
  "mid": "9ba5365b-d652-4de0-b3ac-5954cc2fbdf1",
  "typ": "performance.pdp_visits",
  "bdy": {
      "shop_id": "gid://shopify/Shop/50975277226",
      "collection_id": "gid://shopify/Collection/235800101034"
  } 
} 
```

Sample response:

```js
{
  "to": "skafos-api-v1-svcs:/",
  "frm": "performance-v1-svcs:/",
  "rmid": "9ba5365b-d652-4de0-b3ac-5954cc2fbdf1",
  "typ": "performance.pdp_visits",
  "bdy": {
     "pdpVisits": [
          {"date": "2021-03-16", "pdpVisits": 1},
          {"date": "2021-03-17", "pdpVisits": 2}
       ]
  }
}
```

### **/v1/performance/top_likes**

Sample request:

```js
{
  "to": "performance-v1-svcs:/",
  "frm": "skafos-api-v1-svcs:/",
  "mid": "9ba5365b-d652-4de0-b3ac-5954cc2fbdf1",
  "typ": "performance.top_likes",
  "bdy": {
      "shop_id": "gid://shopify/Shop/50975277226",
      "collection_id": "gid://shopify/Collection/235800101034"
  } 
} 
```

Sample response:

```js
{
  "to": "skafos-api-v1-svcs:/",
  "frm": "performance-v1-svcs:/",
  "rmid": "9ba5365b-d652-4de0-b3ac-5954cc2fbdf1",
  "typ": "performance.top_likes",
  "bdy": {
    "topLikes": [
                {
                   "id": "gid://shopify/Product/200MTVS176A-V",
                   "product": "Tuscan Baby Blue Dotted Diamond Trellis Nursery Rug",
                   "imageUrl": "https://www.rug-images.com/products/s/200MTVS176A.jpg",
                   "pdpUrl": 'https://www.rugsusa.com/rugsusa/rugs/rugs-usa-dotted-diamond-trellis-nursery/baby-blue/200MTVS176A-P.html',
                   "likes": 94,
                   "rank": 1
                  },
               {
                   "id": "gid://shopify/Product/200YLRM05B-V",
                   "product": "Gothamite Ivory Soft Awning Stripes Rug",
                   "imageUrl": "https://www.rug-images.com/products/s/200YLRM05B.jpg",
                   "pdpUrl": 'https://www.rugsusa.com/rugsusa/rugs/rugs-usa-soft-awning-stripes/ivory/200YLRM05A-P.html',
                   "likes": 87,
                   "rank": 2
                }
           ]
  } 
}
```

### **/v1/performance/top_dislikes**

Sample request:

```js
{
  "to": "performance-v1-svcs:/",
  "frm": "skafos-api-v1-svcs:/",
  "mid": "9ba5365b-d652-4de0-b3ac-5954cc2fbdf1",
  "typ": "performance.top_dislikes",
  "bdy": {
      "shop_id": "gid://shopify/Shop/50975277226",
      "collection_id": "gid://shopify/Collection/235800101034"
  } 
}
```

Sample response:

```js
{
  "to": "skafos-api-v1-svcs:/",
  "frm": "performance-v1-svcs:/",
  "rmid": "9ba5365b-d652-4de0-b3ac-5954cc2fbdf1",
  "typ": "performance.top_dislikes",
  "bdy": {
    "topDislikes": [
                {
                   "id": "gid://shopify/Product/200MTVS176A-V",
                   "product": "Tuscan Baby Blue Dotted Diamond Trellis Nursery Rug",
                   "imageUrl": "https://www.rug-images.com/products/s/200MTVS176A.jpg",
                   "pdpUrl": 'https://www.rugsusa.com/rugsusa/rugs/rugs-usa-dotted-diamond-trellis-nursery/baby-blue/200MTVS176A-P.html',
                   "dislikes": 94,
                   "rank": 1
                  },
               {
                   "id": "gid://shopify/Product/200YLRM05B-V",
                   "product": "Gothamite Ivory Soft Awning Stripes Rug",
                   "imageUrl": "https://www.rug-images.com/products/s/200YLRM05B.jpg",
                   "pdpUrl": 'https://www.rugsusa.com/rugsusa/rugs/rugs-usa-soft-awning-stripes/ivory/200YLRM05A-P.html',
                   "dislikes": 87,
                   "rank": 2
                }
           ]
   }
}
```

### **/v1/performance/top_pdp_visits**

Sample request:

```js
{
  "to": "performance-v1-svcs:/",
  "frm": "skafos-api-v1-svcs:/",
  "mid": "9ba5365b-d652-4de0-b3ac-5954cc2fbdf1",
  "typ": "performance.top_pdp_visits",
  "bdy": {
      "shop_id": "gid://shopify/Shop/50975277226",
      "collection_id": "gid://shopify/Collection/235800101034"
  } 
}
```

Sample response:

```js
{
  "to": "skafos-api-v1-svcs:/",
  "frm": "performance-v1-svcs:/",
  "rmid": "9ba5365b-d652-4de0-b3ac-5954cc2fbdf1",
  "typ": "performance.top_pdp_visits",
  "bdy": {
    "topPdpVisits": [
                {
                   "id": "gid://shopify/Product/200MTVS176A-V",
                   "product": "Tuscan Baby Blue Dotted Diamond Trellis Nursery Rug",
                   "imageUrl": "https://www.rug-images.com/products/s/200MTVS176A.jpg",
                   "pdpUrl": 'https://www.rugsusa.com/rugsusa/rugs/rugs-usa-dotted-diamond-trellis-nursery/baby-blue/200MTVS176A-P.html',
                   "pdpVisits": 94,
                   "rank": 1
                  },
               {
                   "id": "gid://shopify/Product/200YLRM05B-V",
                   "product": "Gothamite Ivory Soft Awning Stripes Rug",
                   "imageUrl": "https://www.rug-images.com/products/s/200YLRM05B.jpg",
                   "pdpUrl": 'https://www.rugsusa.com/rugsusa/rugs/rugs-usa-soft-awning-stripes/ivory/200YLRM05A-P.html',
                   "pdpVisits": 87,
                   "rank": 2
                }
           ]
   }
}
```

## Future

* Date range query (possibly up to X days in the past)
  * v1 is set at 14 days
* Counts query for top likes/top dislikes
  * v1 is set at 10
