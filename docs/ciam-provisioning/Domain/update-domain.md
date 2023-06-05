# Update Domain 

- Provisioning API provides a REST API to Update a Domain.

There are steps required at the application-side that should meet the below criteria:  

- Can make http/REST calls  

- Has the application Id of an application

- Has the OAuth2 client credentials generated via application.client scope

<!--
type: tab
titles: Request, Response
-->

The below table identifies the parameter required for Domain payload.

| Variable | Type | Maximum Length | Required | Description |
| -------- | -- |------------| ------- | ---- |
| `domainId` | *string* | - | &#10004; | A unique ID used to identify a domain. |

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

<!-- type: tab-end -->