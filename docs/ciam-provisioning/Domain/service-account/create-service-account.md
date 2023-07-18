# Create Domain Service Account

- Provisioning API provides a REST API to create a Domain Service Account.

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
| `friendlyName` | *string* | - | - | friendly name for domain Service Account. |
| `surname` | *string* | - | &#10004; | surname for domain Service Account. |
| `givenName` | *string* | - | - | given name domain Service Account. |
| `description` | *string* | - | - | description for domain Service Account. |

### Example of Create Domain Service Account payload

```json
{
   "friendlyName": "TEST_SVCACT_{{$randomInt}}",
   "surname": "SVCACT {{$randomInt}}",
   "givenName": "TEST {{$randomInt}}",
   "description": "{{UAID}} Service Account",
   "extendedAttr1":[
       "a","b","c"
   ],
   "extendedAttr2":[
       "d","e","f"
   ],
   "extendedAttr3": "FISV",
   "extendedAttr4": "WEB",
   "extendedAttr5": "NOW100",
   "extendedAttr6": "NOW",
   "extendedAttr7": "smsmicro",
   "extendedAttr8": "10.194.138.30",
   "extendedAttr9": "26025"
}
```
<!--
type: tab
-->

### Example of Create Domain Service Account (200: Created) response

```json
{
    "accountId": "S1it658uo",
    "friendlyId": "Dan8g3fte.TEST_SVCACT_723",
    "friendlyName": "TEST_SVCACT_723",
    "surname": "SVCACT 785",
    "givenName": "TEST 369",
    "userPassword": "2b|teT^QA}",
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
    "transactionId": "958447eb-b9cb-431c-8cf9-c5e48552c3a7",
    "owner": [
        "Atithgwm6"
    ]
}
```

<!-- type: tab-end -->