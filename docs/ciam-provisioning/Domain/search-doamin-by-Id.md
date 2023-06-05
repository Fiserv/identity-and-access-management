# Search Domain By ID

- Provisioning API provides a REST API to search a domain by domain Id.

There are steps required at the application-side that should meet the below criteria:  

- Can make http/REST calls  

- Has the application Id of an application

- Has the OAuth2 client credentials generated via application.client scope


<!--
type: tab
titles: Request, Response
-->

- Search domain provides the domain details for a specific domain Id.

The below table identifies the parameter required for Domain domain payload.

| Variable | Type | Maximum Length | Required | Description |
| -------- | -- |------------| ------- | ---- |
| `domainId` | *string* | - | &#10004; | A unique ID used to identify the domain. |


<!--
type: tab
-->

### Example of Search Domain By Domain Id (200: Created) response

```json

{
  "schemas": [
    "string"
  ],
  "resourceType": "string",
  "transactionId": "string",
  "owner": [
    "string"
  ],
  "domainId": "string",
  "friendlyId": "string",
  "friendlyName": "string",
  "surname": "string",
  "givenName": "string",
  "userPassword": "string",
  "description": "string",
  "extendedAttr1": [
    "string"
  ],
  "extendedAttr2": [
    "string"
  ],
  "extendedAttr3": "string",
  "extendedAttr4": "string",
  "extendedAttr5": "string",
  "extendedAttr6": "string",
  "extendedAttr7": "string",
  "extendedAttr8": "string",
  "extendedAttr9": "string"
}

```

<!-- type: tab-end -->