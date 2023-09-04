## Create Risk Policy

<!--
type: tab
titles: Request, Response
-->

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