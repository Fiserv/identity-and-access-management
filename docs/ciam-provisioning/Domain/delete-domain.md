# Delete Domain 

- Provisioning API provides a REST API to delete a Domain.

There are steps required at the application-side that should meet the below criteria:  

- Can make http/REST calls  

- Has the application Id of an application

- Has the OAuth2 client credentials generated via application.client scope

<!--
type: tab
titles: Request, Response
-->

The below table identifies the parameter required for delete domain call.

| Variable | Type | Maximum Length | Required | Description |
| -------- | -- |------------| ------- | ---- |
| `domainId` | *string* | - | &#10004; | A unique ID used to identify the domain. |


<!--
type: tab
-->

### Example of Delete  (204: No Content) response

- Once deleted the  successfully, it returns 204 response code with no body.


<!-- type: tab-end -->