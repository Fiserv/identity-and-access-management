## Enable FIDO2 

To enable/disable FIDO2 services.

<!--
type: tab
titles: Request, Response
-->

Endpoint **:**

**Put** [app-reg/v1/fido2Service/ServiceAccount/{{svc_acc}}/config](../api/?type=put&path=/app-reg/v1/fido2Service/ServiceAccount/{svc_acc}/config&version=2.0.0)

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

### 200-OK Response example

**If enableFIDO2 is true in payload**

```json
{
    "message": "FIDO2 Service has been now enabled for your application."
}

**If enableFIDO2 is false in payload**

```json
{
    "message": "FIDO2 Service has been now disabled for your application."
}

<!-- type: tab-end -->