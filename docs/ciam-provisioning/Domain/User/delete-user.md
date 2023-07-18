# Delete Domain User

- Provisioning API provides a REST API to delete a Domain User.

There are steps required at the application-side that should meet the below criteria:  

- Can make http/REST calls  

- Has the application Id of an application

- Has the OAuth2 client credentials generated via application.client scope

<!--
type: tab
titles: Request, Response
-->

The below table identifies the parameter required for Domain User payload.

| Variable | Type | Maximum Length | Required | Description |
| -------- | -- |------------| ------- | ---- |
| `domainId` | *string* | - | &#10004; | A unique ID used to identify which domain the User belongs to. |
| `userId` | *string* | - | &#10004; | A unique ID used to identify the User. |


<!--
type: tab
-->

### Example of Delete User (204: No Content) response

- Once deleted the User successfully, it returns 204 response code with no body.


<!-- type: tab-end -->