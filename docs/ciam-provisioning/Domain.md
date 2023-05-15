# Domain APIs

- CIAM Provisioning provides the REST endpoints to perform the domain operations on directory like search all domains, create a domain, search a domain, update a domain, delete a domain.

There are steps required at the application-side that should meet the below criteria:  
- Can make http/REST calls  
- Has the registered application details   


---  

- [Step 1: Getting an access token](#step-1-getting-an-access-token)  

- [Step 2: Domain CRUD operations](#step-2-domain-crud-operations)  

---

## Step 1: Getting an access token 

- Access tokens are credential strings that represent authorization to access a protected resource. Applications obtain access tokens by making OAuth connect requests to an authorization server; CIAM Provisioning API resource servers require clients to authenticate using access tokens. Access tokens are obtained from the token endpoint (when using the client credentials grant type).

- Scopes are used to grant an application different levels of access to data on behalf of the end user. Each API may declare one or more scopes. 

Here are the list of allowed scopes:
- application.client 
Application client scope for allowed CIAM Provisioning API ACL

- application.client domain.manage
Application client scope allowed for Delete of App Owned Domain

- iam.root
Root scope used to onboard applications

To get an access token, the following must be true:  

- The application is configured via onboarding process.

- The credentials are provided to application owner for getting an access token.  

- The application runtime has access to the client secret and token endpoint.



## Step 2: Domain CRUD operations 

- Create Domain

<!--
type: tab
titles: Request, Response
-->

### Example of Create Domain payload

```json
{
    "friendlyName": "UAID-12333_Foo Inc",
    "description": "UAID-12333 domain description"
}

```
<!--
type: tab
-->

### Example of Create Domain (200: Created) response

<!-- theme: info -->
> See [Response Handling](?path=docs/Resources/Guides/Response-Codes/Response-Handling.md) for more information.

```json
{
    "domainId": "9d77e19c-ab9a-4820-bdb8-924cd5aad2ee",
    "hasApplicationIds": [
        "Acrvzwdh0"
    ],
    "description": "UAID-12333 domain description",
    "friendlyName": "UAID-12333_Foo Inc",
    "owner": [
        "Acrvzwdh0"
    ]
}
```

- Search Domain
    Search domain provides the list of available domains.

- Search Domain By Id
    This search gives us the domain details for an specific domain Id.

- Update Domain

<!--
type: tab
titles: Request, Response
-->

### Example of Update Domain payload

```json
{
    "description": "UAID-99999 domain description update",
    "friendlyName": "UAID-99999_domain_name_update"
}

```
<!--
type: tab
-->

### Example of Update Domain (200: Created) response

<!-- theme: info -->
> See [Response Handling](?path=docs/Resources/Guides/Response-Codes/Response-Handling.md) for more information.

```json
{
    "domainId": "Dp8lnk37l",
    "applicationIds": [],
    "creationDate": "2022-05-13T20:26:18.052Z",
    "description": "UAID-99999 domain description update",
    "friendlyName": "UAID-99999_domain_name_update",
    "transactionId": "de4b3f1f-7f17-49ff-b9c0-15aa5a46bb7d"
}

```


- Delete Domain
    Similar to search domain by Id we have delete domain which deletes the domain using domain Id.
