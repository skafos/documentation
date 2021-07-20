# Authentication

## Endpoint

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
  "statusCode": 503,
  "statusMessage": "Service Unavailable",
  "statusDescription": "The server is currently unable to handle the request due to a temporary overloading or maintenance of the server. The implication is that this is a temporary condition which will be alleviated after some delay",
  "result": {
    "reason": "Unavailable auth-svcs instances"
  }
}
```

| statusCode | statusDescription                             |
|------------|-----------------------------------------------|
| 400        | Request is invalid, missing parameters        |
| 401        | User isn"t authorized to access this resource |
| 500        | Internal service error: {“error”:}            |
| 503        | Service Unavailable                           |
