## Register FIDO2 Device
API to Register a FIDO2 device to the specified user resource for passwordless authetication. When a user wants to pair FIDO2 supported biometrics device like MOBILE/YUBIKY/PLATFORM, one can initiates the FIDO2 device Regsitration process with this API, In return we get returns public key credentials required to g
 
  Devices with a status of ACTIVATION_REQUIRED are activated with a valid attestation and origin.

<!--
type: tab
titles: Request, Response
-->

Attributes used in Payload of request are as:

| Variable | Type | Required | Description |
| -------- | ---- | -------- | ----------- |
| `deviceType` | *string* | &#10004; | The type of device which user want to register for MFA.
  Note: irespective of device type user wants to register MOBILE/YUBIKY/PLATFORM
  for FIDO2 device registration fields value will always be "FIDO2". |
| `rp.id` | *string* | &#10004; | The ID of the relying party, used for logging in without having to provide a password. The value of the field should be a domain name, such as sample.com / fiserv.com |
| `rp.name` | *string* | &#10004; | The relying party's human-readable display name (for example, acme). |
| `email` | *string* | &#10004; | Email Address |

### Example Payload to Create MFA Device

```json
{
    "deviceType": "FIDO2",
    "rp": {
        "id": "app.fiserv.com",
        "name": "CartApp"
    },
    "email": "wellsforgo.com"
}
```
<!--
type: tab
-->

### Example of Create MFA Device (201: Created) response

```json
{
    "authId": "67e07830-3636-4479-a407-da0a16b85c3c",
    "deviceType": "FIDO2",
    "status": "ACTIVATION_REQUIRED",
    "rp": {
        "id": "pingone.com",
        "name": "pingone.com"
    },
    "publicKeyCredentialCreationOptions": "{"rp":{"id":"pingone.com","name":"pingone.com"},"user":{"id":[-121,2,76,83,98,-86,-48,1,-114,31,-30,-9,116,52,-37,-78,68,-51,63,37,14,68,-112,56,-104,-7,-41,-116,-121,-46,-38,22],"displayName":"APM_NA_TEST_RUN_2102231126$demouser","name":"APM_NA_TEST_RUN_2102231126$demouser"},"challenge":[-19,41,45,-102,-21,109,-109,-125,32,121,-4,-78,-123,80,53,58,81,29,-111,81,75,11,-44,73,-81,90,4,42,-27,108,75,20],"pubKeyCredParams":[{"type":"public-key","alg":"-7"},{"type":"public-key","alg":"-37"},{"type":"public-key","alg":"-257"}],"timeout":120000,"excludeCredentials":[],"authenticatorSelection":{"residentKey":"required","requireResidentKey":true,"userVerification":"required"},"attestation":"none"}"
}

```
<!-- type: tab-end -->