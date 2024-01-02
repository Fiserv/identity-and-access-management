## Read MFA Devices
API to return list of registered mfa devices for the particular user, only FIDO2 and TOTP devices.


<!--
type: tab
titles: Request, Response
-->

Endpoint **:**

**GET** [{{base_url}}/ciam-mfa/v2/users/{{username}}/mfadevices](../api/?type=get&path=/users/{username}/mfadevices&version=2.0.0)

**Payload** **:**

### No Payload since it is a GET call

<!--
type: tab
-->

### Example Response (200: OK)
```json
[
    {
        "deviceType": "FIDO2",
        "status": "ACTIVE",
        "createdAt": "2023-09-26T12:58:34.587Z",
        "rp": {
            "id": "app.fiserv.com",
            "name": "fiserv"
        }
    },
    {
        "deviceType": "TOTP",
        "status": "ACTIVE",
        "deviceName": "samsung",
        "createdAt": "2023-10-11T06:09:48.563Z"
    }
]

```
<!-- type: tab-end -->