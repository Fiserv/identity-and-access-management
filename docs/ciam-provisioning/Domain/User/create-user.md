# Create Domain User

- Provisioning API provides a REST API to create a Domain User.

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
| `friendlyName` | *string* | - | - | friendly name for domain User. |
| `surname` | *string* | - | &#10004; | surname for domain User. |
| `givenName` | *string* | - | - | given name domain User. |
| `description` | *string* | - | - | description for domain User. |

### Example of Create Domain User payload

```json
{
  "friendlyName": "UserName",
  "displayName": "FullName",
  "surname": "LastName",
  "givenName": "FirstName",
  "middleInitial": "u",
  "description": "UAID Domain User",
  "userType": "JobType",
  "emails": [
    {
        "value": "Email"
    }
  ],
  "phoneNumbers": [ 
     {
        "value": "PhoneNumber"
     }
  ],
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

### Example of Create Domain User (200: Created) response

```json
{
    "userId": "Ugewj721x",
    "description": "UAID Domain User",
    "displayName": "FullName",
    "emails": [
        {
            "value": "Email"
        }
    ],
    "friendlyId": "D0jr9dhrg.UserName",
    "friendlyName": "UserName",
    "givenName": "FirstName",
    "middleInitial": "u",
    "password": "r#YJ6apTc*",
    "phoneNumbers": [
        {
            "value": "9876543210"
        }
    ],
    "surname": "LastName",
    "userType": "JobType",
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
    "transactionId": "5e3b4d94-181e-46af-ad69-a54b7f686bd8",
    "owner": [
        "Axnckgl2v"
    ]
}

```

<!-- type: tab-end -->