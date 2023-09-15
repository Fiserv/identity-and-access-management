## Check Device Type of MFA Device

API to check the device type of the registered MFA Device.

### API Parameters

Takes 'type' as query parameter.

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

```json
{
    "deviceType": "TOTP",
    "status": "ACTIVE",
    "deviceName": "iphone",
    "createdAt": "2023-08-31T09:31:30.610Z"
}
```
<!-- type: tab-end -->