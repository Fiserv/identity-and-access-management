# Search Service Account By ID

- Provisioning API provides a REST API to search a Service Account by account Id in the specified domain.

There are steps required at the application-side that should meet the below criteria:  

- Can make http/REST calls  

- Has the application Id of an application

- Has the OAuth2 client credentials generated via application.client scope


<!--
type: tab
titles: Request, Response
-->

- Search Service Account provides the a Service Account details for a specific Service Account Id.

The below table identifies the parameter required for Domain Service Account payload.

| Variable | Type | Maximum Length | Required | Description |
| -------- | -- |------------| ------- | ---- |
| `domainId` | *string* | - | &#10004; | A unique ID used to identify the domain to which the Service Account belongs. |
| `accountId` | *string* | - | &#10004; | A unique ID used to identify the Service Account. |


<!--
type: tab
-->

### Example of Search Service Account by Id (200: Created) response

```json

{
    "accountId": "Skc8o2t41",
    "friendlyId": "Dan8g3fte.TEST_SVCACT_7",
    "friendlyName": "TEST_SVCACT_7",
    "surname": "SVCACT 277777",
    "givenName": "TEST 854",
    "description": "UAID-17999 Service Account",
    "extendedAttr1": [
        "a",
        "b",
        "c"
    ],
    "extendedAttr2": [
        "d",
        "e",
        "f"
    ],
    "extendedAttr3": "FISV7777777",
    "extendedAttr4": "WEB",
    "extendedAttr5": "NOW100",
    "extendedAttr6": "NOW",
    "extendedAttr7": "smsmicro",
    "extendedAttr8": "10.194.138.30",
    "extendedAttr9": "26025",
    "transactionId": "c37ef532-1d61-4790-85e2-e039db1d07b2",
    "owner": [
        "Atithgwm6"
    ]
}

```

<!-- type: tab-end -->