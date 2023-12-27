---
tags: [CIAM, Provisioning API, Register Application]
---

# Initial application setup

<!--theme: warning -->
> IAM Service Team register the application. The API requires admin credentials to generate the OAuth token needed for application registration.

---

- Provisioning API provides a REST endpoint to create an Application with the specified domain client, in return the API provides the on-boarded application details. The application detail contains the application Id, roles, permissions, client Id and client secret. The same client Id and secret would be used to generate the session token using OAuth2 required for all operations.

There are steps required at the application-side that should meet the below criteria:  

- Can make http/REST calls  

- Has the UAID and domain Id to create an application


## Register Application    

<!--
type: tab
titles: Request, Response
-->

The below table identifies the parameter required for `Application OAuth Client`.

| Variable | Type | Maximum Length | Required | Description |
| -------- | -- |------------| ------- | ---- |
| `uaid` | *string* | - | &#10004; | A unique ID used to identify the application. |
| `friendlyName` | *string* | - | &#10004; | provide a friendlyName for the application. |
| `presentationAddress` | *string* | - | &#10004; | domain name for application. |
| `description` | *string* | - | &#10004; | a brief description about the application. |
| `redirectUrls` | *list* | - | &#10004; | redirect url for the application. |

**Payload :**

```json
{
   "uaid": "UAID-99999",
   "friendlyName": "UAID-99999_Application",
   "presentationAddress": "https://DomainName",
   "description": "UAID-99999 Application Description",
   "redirectUrls" : [ "https://localhost:8443", "https://google.com" ]
}
```
<!--
type: tab
-->

### Example of create an application (200: OK) response

```json
{
    "idmAccount": {
        "accountId": "Se11mc3as",
        "friendlyId": "Se11mc3as",
        "friendlyName": "IDM account for app Axnckgl2v",
        "surname": "IDM account for app Axnckgl2v",
        "givenName": "IDM account for app Axnckgl2v",
        "userPassword": "xxxxxxxxxx",
        "application": {
            "applicationId": "Axnckgl2v",
            "presentationAddress": "https://DomainName",
            "redirectUrls": [
                "https://localhost:8443",
                "https://google.com"
            ],
            "friendlyName": "UAID-99999_Application",
            "description": "UAID-99999 Application Description",
            "uaid": "UAID-99999",
            "owner": [
                "Axnckgl2v"
            ]
        },
        "roles": [
            {
                "roleId": "Rcps37ybs",
                "friendlyId": "Axnckgl2v.iam.application.admin",
                "friendlyName": "iam.application.admin",
                "description": "FiServ IAM Application Administrator",
                "permissions": [
                    {
                        "permissionId": "iam.role.manage",
                        "description": "iam role manage",
                        "owner": [
                            "Axnckgl2v"
                        ]
                    },
                    {
                        "permissionId": "serviceaccount.manage",
                        "description": "serviceaccount manage",
                        "owner": [
                            "Axnckgl2v"
                        ]
                    },
                    {
                        "permissionId": "domain.manage",
                        "description": "domain manage",
                        "owner": [
                            "Axnckgl2v"
                        ]
                    }
                ],
                "owner": [
                    "Axnckgl2v"
                ]
            }
        ],
        "owner": [
            "Axnckgl2v"
        ]
    },
    "permissions": [
        {
            "permissionId": "iam.role.manage",
            "description": "iam role manage",
            "owner": [
                "Axnckgl2v"
            ]
        },
        {
            "permissionId": "serviceaccount.manage",
            "description": "serviceaccount manage",
            "owner": [
                "Axnckgl2v"
            ]
        },
        {
            "permissionId": "domain.manage",
            "description": "domain manage",
            "owner": [
                "Axnckgl2v"
            ]
        }
    ],
    "roles": [
        {
            "owner": [
                "Axnckgl2v"
            ],
            "roleId": "Rcps37ybs",
            "friendlyId": "Axnckgl2v.iam.application.admin",
            "friendlyName": "iam.application.admin",
            "description": "FiServ IAM Application Administrator"
        }
    ],
    "transactionId": "b39d0def-5cb4-401b-bc78-2b46eedf7993",
    "owner": [],
    "applicationId": "Axnckgl2v",
    "presentationAddress": "https://DomainName",
    "redirectUrls": [
        "https://localhost:8443",
        "https://google.com"
    ],
    "friendlyName": "UAID-99999_Application",
    "description": "UAID-99999 Application Description",
    "secret": "xxxxxxxxxxxxxxxxxxxxxxxxxxx"
}
```
<!-- type: tab-end -->