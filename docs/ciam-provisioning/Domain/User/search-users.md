# Search Users

- Provisioning API provides a REST API to search all Users in the specified domain.

There are steps required at the application-side that should meet the below criteria:  

- Can make http/REST calls  

- Has the application Id of an application

- Has the OAuth2 client credentials generated via application.client scope


<!--
type: tab
titles: Request, Response
-->

- Search User provides the list of available Users in a domain.

The below table identifies the parameter required for Domain User payload.

| Variable | Type | Maximum Length | Required | Description |
| -------- | -- |------------| ------- | ---- |
| `domainId` | *string* | - | &#10004; | A unique ID used to identify the domain to which the User belongs. |


<!--
type: tab
-->

### Example of Search Users (200: Created) response

```json

[
    {
        "userId": "U61ocifws",
        "parentContainer": "Users",
        "friendlyId": "Dan8g3fte.Madaline2666666",
        "friendlyName": "Madaline2666666",
        "orgFriendlyName": "UAID-17999_jon_domain_name",
        "surname": "Ebert",
        "owner": [
            "Atithgwm6"
        ]
    },
    {
        "userId": "U8kdp0bmc",
        "parentContainer": "Users",
        "friendlyId": "Dan8g3fte.Lila.Williamson",
        "friendlyName": "Lila.Williamson",
        "orgFriendlyName": "UAID-17999_jon_domain_name",
        "surname": "Weissnat",
        "owner": [
            "Atithgwm6"
        ]
    },
    {
        "userId": "Uwtc5blfi",
        "parentContainer": "Users",
        "friendlyId": "Dan8g3fte.Daija_OHara19",
        "friendlyName": "Daija_OHara19",
        "orgFriendlyName": "UAID-17999_jon_domain_name",
        "surname": "Rodriguez",
        "owner": [
            "Atithgwm6"
        ]
    },
    {
        "userId": "Uvo5n5ghh",
        "parentContainer": "Users",
        "friendlyId": "Dan8g3fte.Watson_Schoen92",
        "friendlyName": "Watson_Schoen92",
        "orgFriendlyName": "UAID-17999_jon_domain_name",
        "surname": "Kessler",
        "owner": [
            "Atithgwm6"
        ]
    },
    {
        "userId": "Ug7bjrgbz",
        "parentContainer": "Users",
        "description": "UAID-17999 Domain User",
        "displayName": "Ms. Marian Olson",
        "emails": [
            {
                "value": "Pietro_Flatley@yahoo.com"
            }
        ],
        "friendlyId": "Dan8g3fte.Madison46",
        "friendlyName": "Madison46",
        "givenName": "Antonia",
        "middleInitial": "e",
        "orgFriendlyName": "UAID-17999_jon_domain_name",
        "phoneNumbers": [
            {
                "value": "320-969-1531"
            }
        ],
        "surname": "Schuppe",
        "userType": "Architect",
        "extendedAttr3": "ext3",
        "extendedAttr4": "ext4",
        "owner": [
            "Atithgwm6"
        ]
    }
]

```

<!-- type: tab-end -->