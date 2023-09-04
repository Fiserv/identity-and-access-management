## Risk Service Configuration

<!--
type: tab
titles: Request, Response
-->

### Payload to Register App

##### If specific policyId is provided to enable/disable

```json
{
    "enableRisk": true,
    "policyID": {{policyId}}
}
```

##### If no policyId provided to enable/disable (default policy would be enabled)

```json
{
    "enableRisk": true
}
```

##### Client trying to diable already disabled policy

```json
{
    "enableRisk": false,
    "policyID": {{policyId}}
}
```
<!--
type: tab
-->

###  (201: Created) response example

##### If specific policyId is provided to enable/disable

Risk Service has been now enabled/diabled for your application

##### If no policyId provided to enable/disable (default policy would be enabled)

Risk Service has been now enabled/diabled for your application

##### Client trying to diable already disabled policy

```json
{
    "error": 10001,
    "message": "INVALID_DATA",
    "traceID": "47cb31c3-38f6-4b01-a9eb-8e2802d3a609",
    "timestamp": "Sep-04-2023 05:14:07.191 +0000",
    "details": "Risk Service for your application has not been enabled yet"
}
```
<!-- type: tab-end -->