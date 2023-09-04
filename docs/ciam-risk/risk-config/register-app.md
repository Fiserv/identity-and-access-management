## Register App

<!--
type: tab
titles: Request, Response
-->

### Payload to Register App

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

###  (201: Created) response example

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