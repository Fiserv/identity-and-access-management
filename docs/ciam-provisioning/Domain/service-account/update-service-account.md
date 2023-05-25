# Update Domain Service Account

- Provisioning API provides a REST API to Update a Domain Service Account.

There are steps required at the application-side that should meet the below criteria:  

- Can make http/REST calls  

- Has the application Id of an application

- Has the OAuth2 client credentials generated via application.client scope

<!--
type: tab
titles: Request, Response
-->

The below table identifies the parameter required for Domain Service Account payload.

| Variable | Type | Maximum Length | Required | Description |
| -------- | -- |------------| ------- | ---- |
| `accountId` | *string* | - | &#10004; | A unique ID used to identify the Service Account. |
| `domainId` | *string* | - | &#10004; | A unique ID used to identify a domain. |

### Example of Update Domain Service Account payload

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
        "c",
        "d"
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
<!--
type: tab
-->

### Example of Update Domain Service Account (200: Created) response

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
        "c",
        "d"
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
    "transactionId": "8be5071b-9828-4ceb-a646-98b4ac75a27b",
    "owner": [
        "Atithgwm6"
    ]
}

```

<!-- type: tab-end -->