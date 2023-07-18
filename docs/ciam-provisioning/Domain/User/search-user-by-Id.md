# Search User By ID

- Provisioning API provides a REST API to search a User by User Id in the specified domain.

There are steps required at the application-side that should meet the below criteria:  

- Can make http/REST calls  

- Has the application Id of an application

- Has the OAuth2 client credentials generated via application.client scope


<!--
type: tab
titles: Request, Response
-->

- Search User provides the User details for a specific User Id.

The below table identifies the parameter required for Domain User payload.

| Variable | Type | Maximum Length | Required | Description |
| -------- | -- |------------| ------- | ---- |
| `domainId` | *string* | - | &#10004; | A unique ID used to identify the domain to which the User belongs. |
| `UserId` | *string* | - | &#10004; | A unique ID used to identify the User. |


<!--
type: tab
-->

### Example of Search User by Id (200: Created) response

```json

{
    "userId": "Um9tr9hu7",
    "parentContainer": "Users",
    "friendlyId": "D4al7ke92.Um9tr9hu7",
    "orgFriendlyName": "UAID-99999_domain_name_update",
    "surname": "Wilkinson",
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
    "transactionId": "01b3d5df-120e-41c8-ab0a-e4408e3b558f",
    "owner": [
        "A1dsnzk20"
    ]
}

```

<!-- type: tab-end -->