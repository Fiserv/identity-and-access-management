# Application OAuth Client

- Provisioning API provides a REST endpoints to update OAuth client settings.

There are steps required at the application-side that should meet the below criteria:  

- Can make http/REST calls  

- Has the application Id of an application

- Has the OAuth2 client credentials generated via application.client scope


## Get Application OAuth Client Settings    

<!--
type: tab
titles: Request, Response
-->

The below table identifies the parameter required for `Application OAuth Client`.

| Variable | Type | Maximum Length | Required | Description |
| -------- | -- |------------| ------- | ---- |
| `applicationId` | *string* | - | &#10004; | A unique ID used to identify the Application, This will be created by application after successful application registration. |
| `request body` | *object* | - | &#10004; | Request payload having attributes that needs to be changed. |

### Example of Update OAuth Client request

```json
{
    "name": "UAID-99990_ApplicationTest",
    "description": "UAID-99990 Application DescriptionTest",
    "redirectUrls": [
        "https://localhost:8443",
        "http://google.com"
    ]
}
```

<!--
type: tab
-->

### Example of Update OAuth Client (200: OK) response

```json
{
    "name": "UAID-99990_ApplicationTest",
    "description": "UAID-99990 Application DescriptionTest",
    "redirectUrls": [
        "https://localhost:8443",
        "http://google.com"
    ],
    "transactionId": "c2d12c9b-a554-4afc-b88e-34cd85414fcf"
}

```
<!-- type: tab-end -->
