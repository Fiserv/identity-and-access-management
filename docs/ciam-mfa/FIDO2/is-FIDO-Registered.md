## isFIDO Registered

- Prereqsuite is to get access token.

- Is there a registered Fido device for a specific user?

### API Parameter

Takes only username as the path parameter.

<!--
type: tab
titles: Request, Response
-->

Endpoint to get MFA devices **:**

**GET** [/ciam-mfa/v2/users/{{username}}/isFidoRegistered/{{rpId}}](../api/?type=get&path=/users/{username}/isFidoRegistered/{rpId}&version=2.0.0)

### Example Payload to Authenticate Device

##### No Payload required

<!--
type: tab
-->

### Example of Authenticate Device (200: OK) response

#### 1 - If user itself does not exist 
```json
{
    "status": "FAILURE",
    "message": "User not found, please check the username"
}
```

#### 2 - Not a single device registered for given user.
```json
{
    "status": "FAILURE",
    "message": "No registered FIDO2 Device Found"
}
```

#### 3 - At least one device registered for user.
```json
{
    "status": "SUCCESS",
    "message": "Registered FIDO2 Device Found"
}
```
<!-- type: tab-end -->

