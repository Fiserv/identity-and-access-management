# Search Service Accounts

- Provisioning API provides a REST API to search all Service Accounts in the specified domain.

There are steps required at the application-side that should meet the below criteria:  

- Can make http/REST calls  

- Has the application Id of an application

- Has the OAuth2 client credentials generated via application.client scope


<!--
type: tab
titles: Request, Response
-->

- Search Service Accounts provides the list of available Service Accounts in a domain.

The below table identifies the parameter required for Domain Service Accounts payload.

| Variable | Type | Maximum Length | Required | Description |
| -------- | -- |------------| ------- | ---- |
| `domainId` | *string* | - | &#10004; | A unique ID used to identify the domain to which the Service Accounts belongs. |


<!--
type: tab
-->

### Example of Search Service Accounts (200: Created) response

```json

[
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
        "domain": {
            "domainId": "Dan8g3fte",
            "hasApplicationIds": [
                "Atithgwm6"
            ],
            "creationDate": "2023-02-20T18:42:59.533Z",
            "description": "UAID-17999 Jon domain description",
            "friendlyName": "UAID-17999_jon_domain_name",
            "owner": [
                "Atithgwm6"
            ]
        },
        "owner": [
            "Atithgwm6"
        ]
    },
    {
        "accountId": "Sv7e1nbiq",
        "friendlyId": "Dan8g3fte.TEST_SVCACT_760",
        "friendlyName": "TEST_SVCACT_760",
        "surname": "SVCACT 596",
        "givenName": "TEST 459",
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
        "extendedAttr3": "FISV",
        "extendedAttr4": "WEB",
        "extendedAttr5": "NOW100",
        "extendedAttr6": "NOW",
        "extendedAttr7": "smsmicro",
        "extendedAttr8": "10.194.138.30",
        "extendedAttr9": "26025",
        "domain": {
            "domainId": "Dan8g3fte",
            "hasApplicationIds": [
                "Atithgwm6"
            ],
            "creationDate": "2023-02-20T18:42:59.533Z",
            "description": "UAID-17999 Jon domain description",
            "friendlyName": "UAID-17999_jon_domain_name",
            "owner": [
                "Atithgwm6"
            ]
        },
        "owner": [
            "Atithgwm6"
        ]
    }
]
```

<!-- type: tab-end -->