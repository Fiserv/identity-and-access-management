## Get MFA Devices
API to return list of registerd mfa devices for a specific user.

- get CIAM MFA access token. 

<!--
type: tab
titles: Request, Response
-->

Endpoint to get MFA devices **:**

**GET /ciam-mfa/v2/users/{{username}}/mfadevices**

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
            "id": "localhost",
            "name": "localhost"
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