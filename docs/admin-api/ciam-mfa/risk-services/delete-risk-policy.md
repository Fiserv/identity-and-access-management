## Delete Risk Policy by ID

API to delete any existing Risk Policy. The policyId to be deleted is provided as path parameter. No payload need to be provided.

The below table identifies the parameter required

| Variable | Type | Maximum Length | Required | Description |
| -------- | -- |------------| ------- | ---- |
| `policyId` | *string* | - | &#10004; | A unique ID used to identify the policy. |

<!--
type: tab
titles: Request, Response
-->

Endpoint **:**

**DELETE** [/group/{groupid}/riskPolicy/{policyId}](../api/?type=delete&path=/group/{groupid}/riskPolicy/{policyId}&version=2.0.0)

Payload **:**

#### No payload required

<!--
type: tab
-->

### 204: No Content response


<!-- type: tab-end -->