# Application OAuth Client

- Provisioning API provides a REST endpoints to read OAuth client settings.

There are steps required at the application-side that should meet the below criteria:  

- Can make http/REST calls  

- Has the application Id of an application

- Has the OAuth2 client credentials generated via application.client scope


## Get Application OAuth Client Settings    

<!--
type: tab
titles: Request, Response
-->

The below table identifies the parameter required for `Application OAuth Client`.

| Variable | Type | Maximum Length | Required | Description |
| -------- | -- |------------| ------- | ---- |
| `applicationId` | *string* | - | &#10004; | A unique ID used to identify the Application, This will be created by application after successful application onboarding. |


<!--
type: tab
-->

### Example of Get OAuth Client (200: OK) response

```json
{
  "resourceType": "string",
  "transactionId": "string",
  "owner": [
    "string"
  ],
  "name": "string",
  "description": "string",
  "redirectUrls": [
    "string"
  ],
  "oidcPolicyName": "string",
  "accessTokenMapping": {
    "name": "string",
    "applicationId": "string",
    "accessTokenManagerName": "string",
    "oidcPolicyName": "string",
    "validatorName": "string",
    "attrMappings": [
      {
        "name": "string",
        "attr": "string"
      }
    ],
    "constants": [
      {
        "name": "string",
        "value": "string"
      }
    ]
  }
}
```
<!-- type: tab-end -->