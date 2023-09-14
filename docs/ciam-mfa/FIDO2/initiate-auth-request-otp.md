## Initiate Auth Request OTP

Initiates an MFA device authentication flow.
<!--
type: tab
titles: Request, Response
-->

Attributes used in Payload of request are as:

| Variable | Type | Required | Description |
| -------- | ---- | -------- | ----------- |
| `rpID` | *string* | &#10004; | The ID of the relying party. The value should be a domain name, such as example.com |


### Example Payload to Initiate Auth Request OTP

```json
{
	"userName":"prasad",
    "rpID": "iam-demo.1dc.com",
    "deviceType": "FIDO2"
}
```
<!--
type: tab
-->

### Example of Initiate Auth Request OTP (201: Created) response

```json
{
    "authId": "038273f3-7d84-4c80-9477-99f88646797d",
    "status": "SUCCESS",
    "message": "Please generate the assertion with 'publicKeyCredentialRequestOptions' using Web Authentication API and authenticate FIDO device with assertion",
    "publicKeyCredentialRequestOptions": "{\"challenge\":[13,93,-97,-86,-108,28,22,-98,-9,-53,37,23,-105,-122,-64,-75,57,-88,-13,57,-112,96,-33,42,-119,-72,116,-94,95,-50,-42,99],\"timeout\":120000,\"rpId\":\"iam-demo.1dc.com\",\"allowCredentials\":[{\"type\":\"public-key\",\"id\":[-114,11,-40,2,-85,-109,-107,-126,-25,-5,-80,113,-9,-25,-24,-98,123,27,-25,-34,6,-66,65,-8,60,-88,-56,16,-78,88,-57,-29,0,-93,23,-50,61,-11,-31,-128,-62,-14,-43,-59,-52,33,-110,-127,-60,31,-26,36,-45,77,64,94,-83,56,3,87,-122,-31,94,-107]}],\"userVerification\":\"preferred\"}"
}
```
<!-- type: tab-end -->