## App Registration (Admin Only)

<!--
type: tab
titles: Request, Response
-->

**POST** [/app-reg/admin/v1/registerapp](../api/?type=post&path=/app-reg/admin/v1/registerapp&branch=develop&version=2.0.0)

### Payload that represents the Updated Policy

The payload parameters are as: 

| Variable | Type | Required | Description |
| -------- | -----| -------  | ----------- |
| `apm` | *string* | &#10004; | APM name of the application |
| `appName` | *string* | &#10004; | Application name |
| `uaid` | *string* | &#10004; | uaid of application |
| `id` | *string* | &#10004; | id of the user | 
| `name` | *string* | - | user name |
| `maxUsers` | *string* | &#10004; | maximum number of users for the application |
| `owner` | *string* | &#10004; | email id of the user |
| `enableCIAMRiskServices` | *boolean* | &#10004; | set true to enable risk service, false otherwise |
| `buGroupId` | *string* | &#10004; | Business Unit ID |
| `customCIAMRiskPolicy` | *string* |  &#10004; | custom policy |

```json
{
    "apm": "APM0006238",
    "appName": "MANUAL_TEST_{{current_timestamp}}",
    "uaid": "UAID-10624",
    "id": "{{user_id}}",
    "name": "",
    "maxUsers": "1000",
    "owner": "{{user_email}}",
    "enableCIAMRiskServices": true,
    "buGroupId":"CIAMNPCAO",
    "customCIAMRiskPolicy" : "c7b032a6-bb0b-4dc5-b8e0-ed85bc862012"
}
```
<!--
type: tab
-->

### Example of Update Risk (201: Created) response

```json
{
    "appName": "MANUAL_TEST_20230929172782",
    "owner": "venkatesh.parthasarathy@fiserv.com",
    "uaid": "UAID-10624",
    "ciamRiskSvcAcctFriendlyID": "D4lrivl2w.MANUAL_TEST_20230929172782_CIAM_RISK",
    "ciamRiskEmailStatus": "Email initiated to user successfully"
}
```
<!-- type: tab-end -->