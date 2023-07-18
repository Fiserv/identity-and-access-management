# Update Domain User

- Provisioning API provides a REST API to Update a Domain User.

There are steps required at the application-side that should meet the below criteria:  

- Can make http/REST calls  

- Has the application Id of an application

- Has the OAuth2 client credentials generated via application.client scope

<!--
type: tab
titles: Request, Response
-->

The below table identifies the parameter required for Domain User payload.

| Variable | Type | Maximum Length | Required | Description |
| -------- | -- |------------| ------- | ---- |
| `accountId` | *string* | - | &#10004; | A unique ID used to identify the User. |
| `userId` | *string* | - | &#10004; | A unique ID used to identify the User. |

### Example of Update Domain User payload

```json

{
    "parentContainer": "Users",
    "displayName": "Sherri Hauck",
    "emails": [
        {
            "value": "Keara29@hotmail.com"
        }
    ],
    "friendlyId": "Dp8lnk37l.Dr. Carrie Moore",
    "friendlyName": "Dr. Carrie Moore",
    "givenName": "{{$randomFirstName}}",
    "middleInitial": "T",
    "orgFriendlyName": "UAID-99999_domain_name",
    "phoneNumbers": [],
    "populationUids": [],
    "surname": "Mertz",
    "userType": "Assistant"
}

```
<!--
type: tab
-->

### Example of Update Domain User (200: Created) response

```json

{
    "userId": "U5ik32u2b",
    "parentContainer": "Users",
    "emails": [],
    "friendlyId": "Dp8lnk37l.Dr. Carrie Moore",
    "friendlyName": "Dr. Carrie Moore",
    "phoneNumbers": [],
    "populationUids": [],
    "extendedAttr1": [],
    "extendedAttr2": [],
    "domain": {
        "domainId": "Dp8lnk37l",
        "applicationIds": [],
        "creationDate": "2022-05-13T20:26:18.052Z",
        "description": "UAID-99999 domain description",
        "friendlyName": "UAID-99999_domain_name"
    },
    "transactionId": "878be44d-282e-4f81-8c9e-fd66a11ea9bf"
}
```

<!-- type: tab-end -->