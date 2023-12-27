# Application Token Mapping

- Provisioning API provides a REST endpoints to read Application access token mapping.

There are steps required at the application-side that should meet the below criteria:  

- Can make http/REST calls  

- Has the application Id of an application

- Has the OAuth2 client credentials generated via application.client scope


## Get Application access token mapping    

<!--
type: tab
titles: Request, Response
-->

The below table identifies the parameter required for `Application Token Mapping`.

| Variable | Type | Maximum Length | Required | Description |
| -------- | -- |------------| ------- | ---- |
| `applicationId` | *string* | - | &#10004; | A unique ID used to identify the Application, This will be created by application after successful application registering. |


<!--
type: tab
-->

### Example of Get Application access token mapping (200: OK) response

```json

{
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

```
<!-- type: tab-end -->