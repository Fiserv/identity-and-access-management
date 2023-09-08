## Create MFA Device

API to add a FIDO2 device to the specified user resource.

<!--
type: tab
titles: Request, Response
-->

Parameters Used in Payload of request are as:

| Variable | Type | Required | Description |
| -------- | ---- | -------- | ----------- |
| `deviceType` | *string* | &#10004; | The device type which must be provided. Options: EMAIL, MOBILE, SMS,VOICE, TOTP (third-party TOTP authenticator applications), FIDO2, PLATFORM - FIDO2 bound biometrics devices (deprecated, use FIDO2 instead), SECURITY_KEY - FIDO2 or U2F security key devices (deprecated, use FIDO2 instead) |
| `rp.id` | *string* | &#10004; | The ID of the relying party. The value should be a domain name, such as example.com (in lower-case characters). |
| `rp.name` | *string* | &#10004; | The relying party's human-readable display name (for example, acme). |

### Example Payload to Create MFA Device

```json
{
    "deviceType": "FIDO2",
    "rp": {
        "id": "app.fiserv.com",
        "name": "CartApp"
    }
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
    "publicKeyCredentialCreationOptions": "{\"rp\":{\"id\":\"pingone.com\",\"name\":\"pingone.com\"},\"user\":{\"id\":[-121,2,76,83,98,-86,-48,1,-114,31,-30,-9,116,52,-37,-78,68,-51,63,37,14,68,-112,56,-104,-7,-41,-116,-121,-46,-38,22],\"displayName\":\"APM_NA_TEST_RUN_2102231126$demouser\",\"name\":\"APM_NA_TEST_RUN_2102231126$demouser\"},\"challenge\":[-19,41,45,-102,-21,109,-109,-125,32,121,-4,-78,-123,80,53,58,81,29,-111,81,75,11,-44,73,-81,90,4,42,-27,108,75,20],\"pubKeyCredParams\":[{\"type\":\"public-key\",\"alg\":\"-7\"},{\"type\":\"public-key\",\"alg\":\"-37\"},{\"type\":\"public-key\",\"alg\":\"-257\"}],\"timeout\":120000,\"excludeCredentials\":[],\"authenticatorSelection\":{\"residentKey\":\"required\",\"requireResidentKey\":true,\"userVerification\":\"required\"},\"attestation\":\"none\"}"
}

```
<!-- type: tab-end -->