## Unpair MFA Device
- This API supports "TOTP" and "FIDO2" devices to unpair for a specific user.

- If user gets disbale by any reason, app team should ensure to unpair all regsitred FODO2 devices.

- This API will help to de-registared FIDO2 Devices  for a specific user.


<!--
type: tab
titles: Request, Response
-->

Endpoint to unpair MFA device **:**

**GET /ciam-mfa/v2/users/{{user_name}}/mfadevices/{{device_type}}?code="all"**

### No payload 

<!--
type: tab
-->

### Response: 204 No Response

<!-- type: tab-end -->