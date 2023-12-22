## Register App

API to generate service account and password.

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
<!--
type: tab
titles: Request, Response
-->

Endpoint **:**

**POST** [/app-reg/v2/registerapp](../api/?type=post&path=/registerapp&version=2.0.0)

Payload **:**

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