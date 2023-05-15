# Domain User APIs

- CIAM Provisioning provides the REST endpoints to perform the user operations on directory like search all users, create a user, search a user, update a user, delete a user.

There are steps required at the application-side that should meet the below criteria:  
- Can make http/REST calls  
- Has the registered application details   


---  

- [Step 1: Getting an access token](#step-1-getting-an-access-token)  

- [Step 2: Domain User CRUD operations](#step-2-domain-user-crud-operations)  

---

## Step 1: Getting an access token 

- Access tokens are credential strings that represent authorization to access a protected resource. Applications obtain access tokens by making OAuth connect requests to an authorization server; CIAM Provisioning API resource servers require clients to authenticate using access tokens. Access tokens are obtained from the token endpoint (when using the client credentials grant type).

- Scopes are used to grant an application different levels of access to data on behalf of the end user. Each API may declare one or more scopes. 

Here are the list of allowed scopes:
- application.client 
Application client scope for allowed CIAM Provisioning API ACL

- application.client domain.manage
Application client scope allowed for Delete of App Owned Domain User

- iam.root
Root scope used to onboard applications

To get an access token, the following must be true:  

- The application is configured via onboarding process.

- The credentials are provided to application owner for getting an access token.  

- The application runtime has access to the client secret and token endpoint.



## Step 2: Domain User CRUD operations 

- Create Domain User

<!--
type: tab
titles: Request, Response
-->

### Example of Create Domain User User payload

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

<!-- theme: info -->
> See [Response Handling](?path=docs/Resources/Guides/Response-Codes/Response-Handling.md) for more information.

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
}```

- Search Domain User
    Search Domain User provides the list of available Domain Users.

- Search Domain User By Id
    This search gives us the Domain User details for an specific user Id.

- Update Domain User

<!--
type: tab
titles: Request, Response
-->

### Example of Update Domain User payload

```json
{
    "userId": "Ugewj721x",
    "parentContainer": "Users",
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
    "orgFriendlyName": "99999_domain_name",
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
    "extendedAttr3": "FISV_updated",
    "extendedAttr4": "WEB",
    "extendedAttr5": "NOW100",
    "extendedAttr6": "NOW",
    "extendedAttr7": "smsmicro",
    "extendedAttr8": "10.194.138.30",
    "extendedAttr9": "26025",
    "transactionId": "2920067d-ce70-4eeb-90fe-1fb192a6f51e",
    "owner": [
        "Axnckgl2v"
    ]
}

```
<!--
type: tab
-->

### Example of Update Domain User (200: Created) response

<!-- theme: info -->
> See [Response Handling](?path=docs/Resources/Guides/Response-Codes/Response-Handling.md) for more information.

```json
{
    "userId": "Ugewj721x",
    "parentContainer": "Users",
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
    "orgFriendlyName": "99999_domain_name",
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
    "extendedAttr3": "FISV_updated",
    "extendedAttr4": "WEB",
    "extendedAttr5": "NOW100",
    "extendedAttr6": "NOW",
    "extendedAttr7": "smsmicro",
    "extendedAttr8": "10.194.138.30",
    "extendedAttr9": "26025",
    "transactionId": "1aea21de-6578-4503-94ab-25609f243df6",
    "owner": [
        "Axnckgl2v"
    ]
}

```


- Delete Domain User
    Similar to search Domain User by Id we have delete Domain User which deletes the domain user by User Id.
