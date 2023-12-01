## Enable FIDO2 

To enable/disable FIDO2 services.

<!--
type: tab
titles: Request, Response
-->

Endpoint to enable/disable FIDO2 service **:**

**Put app-reg/v1/fido2Service/ServiceAccount/Sa2l0bvhz/config**

Payload **:**

```json
{
    "enableFIDO2": true
}

```
| Variable | Type | Value | Required | Description |
| -------- | -- |------------| ------- | ---- |
| `enableFIDO2` | *boolean* | true/false | &#10004; | set true to enable the FIDO2 service or false otherwise |

<!--
type: tab
-->

### 201-Created Response example

**If enableFIDO2 is true in payload**

FIDO2 Service has been now enabled for your application.

**If enableFIDO2 is false in payload**

FIDO2 Service has been now disabled for your application.

<!-- type: tab-end -->