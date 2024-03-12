## Unpair TOTP Device

This API is used to unpair any device registered for TOTP authentication.

The path parameters are as: 

| Variable | Type | Required | Description |
| -------- | -----| -------  | ----------- |
| `user_name` | *string* | &#10004; | username |
| `device_name` | *string* | &#10004; | Name of TOTP device |

<!--
type: tab
titles: Request, Response
-->

Endpoint **:**

**DELETE** [{{base_url}}/ciam-mfa/v2/users/{{user_name}}/mfadevices/{{device_type}}/{{device_name}}](../api/?type=delete&path=/ciam-mfa/v2/users/{user_name}/mfadevices/{device_type}/{device_name}&version=2.0.0)

**Payload** **:**

### No payload 

<!--
type: tab
-->

### Response: 204 No Response

<!-- type: tab-end -->