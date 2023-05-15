# Service Account APIs

- CIAM Provisioning provides the REST endpoints to perform the account operations on directory like search all service-accounts, create a service account, search a service account, update service account, delete an account.

There are steps required at the application-side that should meet the below criteria:  
- Can make http/REST calls  
- Has the registered application details   


---  

- [Step 1: Getting an access token](#step-1-getting-an-access-token)  

- [Step 2: Service Account CRUD operations](#step-2-service-account-crud-operations)  

---

## Step 1: Getting an access token 

- Access tokens are credential strings that represent authorization to access a protected resource. Applications obtain access tokens by making OAuth connect requests to an authorization server; CIAM Provisioning API resource servers require clients to authenticate using access tokens. Access tokens are obtained from the token endpoint (when using the client credentials grant type).

- Scopes are used to grant an application different levels of access to data on behalf of the end user. Each API may declare one or more scopes. 

Here are the list of allowed scopes:
- application.client 
Application client scope for allowed CIAM Provisioning API ACL

- application.client domain.manage
Application client scope allowed for Delete of App Owned Service Account

- iam.root
Root scope used to onboard applications

To get an access token, the following must be true:  

- The application is configured via onboarding process.

- The credentials are provided to application owner for getting an access token.  

- The application runtime has access to the client secret and token endpoint.



## Step 2: Service Account CRUD operations 

- Create Service Account

<!--
type: tab
titles: Request, Response
-->

### Example of Create Service Account payload

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

### Example of Create Service Account (200: Created) response

<!-- theme: info -->
> See [Response Handling](?path=docs/Resources/Guides/Response-Codes/Response-Handling.md) for more information.

```json

{
    "accountId": "Symtg9pjr",
    "friendlyId": "D0jr9dhrg.TEST_SVCACT_194",
    "friendlyName": "TEST_SVCACT_194",
    "surname": "SVCACT 390",
    "givenName": "TEST 161",
    "userPassword": "=wY))%<6U!",
    "description": "UAID-12333 Service Account",
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
    "transactionId": "7cc3e8fe-5394-4a65-8238-5af808ec2493"
}

```

- Search Service Account
    Search Service Account provides the list of available Service Accounts.

- Search Service Account By Id
    This search gives us the Service Account details for an specific account Id.

- Update Service Account

<!--
type: tab
titles: Request, Response
-->

### Example of Update Service Account payload

```json

{
    "accountId": "Symtg9pjr",
    "friendlyId": "D0jr9dhrg.TEST_SVCACT_194",
    "friendlyName": "TEST_SVCACT_194",
    "surname": "SVCACT 390",
    "givenName": "TEST 161",
    "description": "UAID-12333 Service Account Updated",
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
    "extendedAttr3": "FISV_Updated",
    "extendedAttr4": "WEB",
    "extendedAttr5": "NOW100",
    "extendedAttr6": "NOW",
    "extendedAttr7": "smsmicro",
    "extendedAttr8": "10.194.138.30",
    "extendedAttr9": "26025",
    "transactionId": "8e74ae6f-1988-46ee-98e3-ffde003e4edf"
}

```
<!--
type: tab
-->

### Example of Update Service Account (200: Created) response

<!-- theme: info -->
> See [Response Handling](?path=docs/Resources/Guides/Response-Codes/Response-Handling.md) for more information.

```json
{
    "accountId": "Symtg9pjr",
    "friendlyId": "D0jr9dhrg.TEST_SVCACT_194",
    "friendlyName": "TEST_SVCACT_194",
    "surname": "SVCACT 390",
    "givenName": "TEST 161",
    "description": "UAID-12333 Service Account Updated",
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
    "extendedAttr3": "FISV_Updated",
    "extendedAttr4": "WEB",
    "extendedAttr5": "NOW100",
    "extendedAttr6": "NOW",
    "extendedAttr7": "smsmicro",
    "extendedAttr8": "10.194.138.30",
    "extendedAttr9": "26025",
    "transactionId": "2d2e82f9-64d9-4e3f-9f46-b8975f6c31a9"
}

```


- Delete Service Account
    Similar to search Service Account by Id we have delete Service Account which deletes the Service Account by account Id.
