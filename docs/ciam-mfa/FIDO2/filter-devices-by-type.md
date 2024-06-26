## Check Device Type of MFA Device

API to check the device type of the registered MFA Device.

### API Parameters

Takes 'type' as query parameter. It takes value out of TOTP or FIDO.

<!--
type: tab
titles: Request, Response
-->

Endpoint **:**

**GET** [{{base_url}}/ciam-mfa/v1/users/{{username}}/mfadevices?type=TOTP](../api/?type=get&path=/users/{username}/mfadevices&branch=develop&version=2.0.0)

**Payload** **:**

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