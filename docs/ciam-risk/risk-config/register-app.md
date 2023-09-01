## Register App

<!--
type: tab
titles: Request, Response
-->

### Payload that represents the Updated Policy

```json
{
    "apm": "APM0006238",
    "appName": "MANUAL_TEST_{{current_timestamp}}",
    "uaid": "UAID-10624",
    "id": "{{user_id}}",
    "name": "",
    "maxUsers": "1000",
    "owner": "{{user_email}}"
}
```
<!--
type: tab
-->

### Example of Update Risk (201: Created) response

```json
{
    "appName": "MANUAL_TEST_20230901151601",
    "owner": "{{user_email}}",
    "uaid": "UAID-10624",
    "svcAcctFriendlyID": "D4lrivl2w.MANUAL_TEST_20230901151601",
    "svcAcctFriendlyName": "MANUAL_TEST_20230901151601",
    "emailStatus": "Email initiation failed"
}
```
<!-- type: tab-end -->