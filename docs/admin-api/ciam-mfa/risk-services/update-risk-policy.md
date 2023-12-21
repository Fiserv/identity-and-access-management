## Update Risk Policy by PolicyId   

API to update any existing risk policy. The policyId of the risk to be updated is provided as path parameter, and the update is provided as payload of the request.

The below table identifies the parameter required

| Variable | Type | Maximum Length | Required | Description |
| -------- | -- |------------| ------- | ---- |
| `policyId` | *string* | - | &#10004; | A unique ID used to identify the policy. |
| `weightBasedPolicy` | *boolean* | true/false | - | If risk to be determined is weight based or score based |
| `appID` | *string* | apm name | &#10004; | Id of the policy |
| `overriddenPredictors` | *list* | list of risk object | - | Specifies critical risks or priority risks |
| `aggregatedPredictors` | *list* | list of score/weight based risk object | - | Specifies score or weights of different risks | 
| `minMaxScoresPerRiskLevel` | *list* | object | - | assign risk based on score/weights interval |
| `defaultRiskLevel` | *string* | default value | &#10004; | sets the default value |

<!--
type: tab
titles: Request, Response
-->

**PUT** [/group/{groupid}/riskPolicy/{policyId}](../api/?type=put&path=/group/{groupid}/riskPolicy/{policyId}&version=2.0.0)

### Payload that represents the Updated Policy

The payload parameters are as: 

```json
{
    "weightBasedPolicy": true,
    "appID": "APM00006238_20230901142048",
    "overriddenPredictors": [
        {
            "condition": true,
            "name": "GEOVELOCITY_ANOMALY",
            "resultLevel": "HIGH"
        },
        {
            "condition": true,
            "name": "ANONYMOUS_NETWORK_DETECTION",
            "resultLevel": "MEDIUM"
        }
    ],
    "aggregatedPredictors": [
        {
            "score": 3,
            "name": "USER_RISK_BEHAVIOR"
        },
        {
            "score": 7,
            "name": "IP_VELOCITY_BY_USER"
        }
    ],
    "minMaxScoresPerRiskLevel": [
        {
            "riskLevel": "MEDIUM",
            "minScore": 30,
            "maxScore": 50
        },
        {
            "riskLevel": "HIGH",
            "minScore": 50,
            "maxScore": 100
        }
    ],
    "defaultRiskLevel": "Low"
}
```
<!--
type: tab
-->

### Example of Update Risk (201: Created) response

```json
{
    "message": "Ping Risk Policy Updated",
    "id": "8af8a047-c97f-4ce1-8f4f-f524f0cd20ce",
    "name": "APM00006238_20230901142048_RISK_POLICY"
}
```
<!-- type: tab-end -->