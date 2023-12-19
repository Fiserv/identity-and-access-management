---
tags: [CIAM, Risk API, Risk Evaluation]
---

# CIAM Risk Evaluations

---
- Use risk evaluations to calculate the risk level and other risk-related details associated with a received event based on the environment's settings and data provided in the event.

- The risk service provides operations to retrieve risk evaluations from risk providers based on a specified risk policy. The risk policy is determined by the customer's specific configuration settings as well as intelligence gathered from common use cases, which are then used in event evaluation to calculate risk scores for received events.

There are steps required at the application-side that should meet the below criteria:  

- Can make http/REST calls  

- The application has the CIAM Risk service enabled

- Has the Risk SDK to collect the signals data from the browser

The below table identifies the parameter required for `Risk Evaluation`.

| Variable | Type | Maximum Length | Required | Description |
| -------- | -- |------------| ------- | ---- |
| `appId` | *string* | - | - | A unique ID used to identify the application. |
| `ipConfig` | *string* | - | &#10004; | The originating IP address of the authentication flow. |
| `userId` | *string* | - | &#10004; | The ID of the user associated with the event. |
| `sessionId` | *string* | - | - | a brief description about the application. |
| `browserCookie` | *string* | - | - | To improve risk analysis, provide the value of a persistent cookie. |
| `browserUserAgent` | *string* | - | &#10004; | The user agent string for the browser. |
| `signalData` | *string* | - | &#10004; | The data collected by the Signals (CIAM Risk) SDK. |

## Risk Evaluation    
<!--
type: tab
titles: Request, Response
-->

**POST /ciam-mfa/v2/riskEvaluations**

### Payload that represents the Risk Evaluation

```json
{
    "appId": "",
    "ipConfig": "115.111.7.122",
    "userId": "FCUBXQ4",
    "sessionId": "",
    "browserCookie": "",
    "browserUserAgent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/114.0.0.0 Safari/537.36 Edg/114.0.1823.67",
    "signalData": "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.eDE=",
    "policyId": "6bf0f9b0-6ba1-0bbf-0175-4ce7a2dcf2fc"
}
```
<!--
type: tab
-->

### Example of Risk Evaluation (201: Created) response

```json
{
    "riskLevel": "HIGH",
    "riskScore": "75.0",
    "evaluationId": "19fb4d99-3332-4c21-88c9-dc3cdb3df5e6"
}
```
<!-- type: tab-end -->