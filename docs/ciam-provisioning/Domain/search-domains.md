# Search Domains

- Provisioning API provides a REST API to search all Domains.

There are steps required at the application-side that should meet the below criteria:  

- Can make http/REST calls  

- Has the application Id of an application

- Has the OAuth2 client credentials generated via application.client scope


<!--
type: tab
titles: Request, Response
-->

- Search Domain provides the list of all available Domains.

<!--
type: tab
-->

### Example of Search Domains (200: Created) response

```json

{
  "totalResults": 0,
  "startIndex": 0,
  "itemsPerPage": 0,
  "Resources": [
    {
      "accountId": "string",
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
      "extendedAttr9": "string",
      "resourceType": "string",
      "transactionId": "string",
      "owner": [
        "string"
      ]
    }
  ]
}

```

<!-- type: tab-end -->