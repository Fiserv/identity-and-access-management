## Create Risk Policy
API to create new Risk Policy. Critical risks are mentioned under overridenPredictors and score to risks are given under aggregatedPredictors.

Parameters Used in Payload of request are as:

| Variable | Type | Value | Required | Description |
| -------- | -- |------------| ------- | ---- |
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

**POST** [/group/{groupid}/riskPolicy](../api/?type=post&path=/group/{groupid}/riskPolicy&version=2.0.0)

### Payload to Create Risk Policy

```json
{
    "weightBasedPolicy": true,
    "appID": "APM00006238_20230901140371",
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
            "score": 5,
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

### Example of Policy Creation (201: Created) response

```json
{
    "message": "Ping Risk Policy Created",
    "id": "8af8a047-c97f-4ce1-8f4f-f524f0cd20ce",
    "name": "APM00006238_20230901140371_RISK_POLICY"
}
```
<!-- type: tab-end -->