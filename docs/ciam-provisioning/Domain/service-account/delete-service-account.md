# Delete Domain Service Account

- Provisioning API provides a REST API to delete a Domain Service Account.

There are steps required at the application-side that should meet the below criteria:  

- Can make http/REST calls  

- Has the application Id of an application

- Has the OAuth2 client credentials generated via application.client scope

<!--
type: tab
titles: Request, Response
-->

The below table identifies the parameter required for Domain Service Account payload.

| Variable | Type | Maximum Length | Required | Description |
| -------- | -- |------------| ------- | ---- |
| `domainId` | *string* | - | &#10004; | A unique ID used to identify which domain the Service Account belongs to. |
| `accountId` | *string* | - | &#10004; | A unique ID used to identify the Service Account. |


<!--
type: tab
-->

### Example of Delete Service Account (204: No Content) response

- Once deleted the Service Account successfully, it returns 204 response code with no body.


<!-- type: tab-end -->