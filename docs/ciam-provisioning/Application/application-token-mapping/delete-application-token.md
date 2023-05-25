# Reset Application Token Mapping

- Provisioning API provides a REST endpoints to reset custom access token mappings to default.

There are steps required at the application-side that should meet the below criteria:  

- Can make http/REST calls  

- Has the application Id of an application

- Has the OAuth2 client credentials generated via application.client domain.manage scope


## Reset access token mapping to default  

<!--
type: tab
titles: Request, Response
-->

The below table identifies the parameter required for `Application Token Mapping`.

| Variable | Type | Maximum Length | Required | Description |
| -------- | -- |------------| ------- | ---- |
| `applicationId` | *string* | - | &#10004; | A unique ID used to identify the Application, This will be created by application after successful application onboarding. |


<!--
type: tab
-->

### Example of Reset access token mapping access token mapping (204: No Content) response

- Once reverted the access settings successfully to default, it returns 204 response code with no body.

<!-- type: tab-end -->