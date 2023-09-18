## isFIDO Registered

Checks if user is registered for FIDO for the given device; and if user has activated any device for FIDO.

### API Parameter

Takes only username as the path parameter.

<!--
type: tab
titles: Request, Response
-->

### Example Payload to Authenticate Device

##### No Payload required

<!--
type: tab
-->

### Example of Authenticate Device (200: OK) response

#### 1 - If user is not even registered for FIDO 
```json
{
    "status": "FAILURE",
    "message": "User not found, please check the username"
}
```

#### 2 - If user is registered but has not activated any device
```json
{
    "status": "FAILURE",
    "message": "No registered FIDO2 Device Found"
}
```

#### 3 - Whne user is registered and has activated FIDO Device 
```json
{
    "status": "SUCCESS",
    "message": "Registered FIDO2 Device Found"
}
```
<!-- type: tab-end -->
