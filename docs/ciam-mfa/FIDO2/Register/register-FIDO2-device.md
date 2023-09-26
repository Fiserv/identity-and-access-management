## Register FIDO2 Device
FIDO2 registration flow uses functions from the Web Authentication API (webauthn API) to manage device registration (pairing) and authentication. The following sample JavaScript code will help you implement the webauthn API for browser-based operations.

## Step 1: Getting an access token     

Access tokens are credential strings that represent authorization to access a protected resource. Applications obtain access tokens by making OAuth 2 or OpenID Connect requests to an authorization server; MFA API resource servers require clients to authenticate using access tokens. Access tokens are obtained from the token endpoint (when using the client credentials grant type).

To get an access token, the following must be true:  

- The application is configured for MFA using  application onboarding process.

- The credentials are provided to application owner for getting an access token.  

- The application runtime  has access to the client secret and token endpoint. 


## Step 2: Create MFA Device - FIDO2 Device

- As a pre-requisite the FIDO2 service must be enabled for application and client browser should be compatible for FIDO2 (WebAuthn).

- API to Create MFA device for user.



<!--
type: tab
titles: Request, Response
-->

Attributes used in Payload of request are as:

| Variable | Type | Required | Description |
| -------- | ---- | -------- | ----------- |
| `deviceType` | *string* | &#10004; | The type of device which user want to register for MFA. Note: irespective of device type user wants to register MOBILE/YUBIKY/PLATFORM for FIDO2 device registration fields value will always be "FIDO2". |
| `rp.id` | *string* | &#10004; | The ID of the relying party, used for logging in without having to provide a password. The value of the field should be a domain name, such as sample.com / fiserv.com |
| `rp.name` | *string* | &#10004; | The relying party's human-readable display name (for example, acme). |
| `email` | *string* | &#10004; | Email Address |

### Example Payload to Create MFA Device

```json
{
    "deviceType": "FIDO2",
    "rp": {
        "id": "app.fiserv.com",
        "name": "fiserv"
    },
    "email": "username.fiserv.com"
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
        "id": "app.fiserv.com",
        "name": "fiserv"
    },
    "publicKeyCredentialCreationOptions": "{"rp":{"id":"pingone.com","name":"pingone.com"},"user":{"id":[-121,2,76,83,98,-86,-48,1,-114,31,-30,-9,116,52,-37,-78,68,-51,63,37,14,68,-112,56,-104,-7,-41,-116,-121,-46,-38,22],"displayName":"APM_NA_TEST_RUN_2102231126$demouser","name":"APM_NA_TEST_RUN_2102231126$demouser"},"challenge":[-19,41,45,-102,-21,109,-109,-125,32,121,-4,-78,-123,80,53,58,81,29,-111,81,75,11,-44,73,-81,90,4,42,-27,108,75,20],"pubKeyCredParams":[{"type":"public-key","alg":"-7"},{"type":"public-key","alg":"-37"},{"type":"public-key","alg":"-257"}],"timeout":120000,"excludeCredentials":[],"authenticatorSelection":{"residentKey":"required","requireResidentKey":true,"userVerification":"required"},"attestation":"none"}"
}

```
<!-- type: tab-end -->

## Step 3: Device pairing

Call the `navigator.credentials.create` method using the publicKeyCredentialOptions value returned from the Create MFA Device API:


```javascript

var authAbortController = window.PublicKeyCredential ? new AbortController() : null;
var authAbortSignal = window.PublicKeyCredential ? authAbortController.signal : null;

window.abortWebAuthnSignal = function abortWebAuthnSignal() {
    authAbortController.abort();
    authAbortController = new AbortController();
    authAbortSignal = authAbortController.signal;
}

window.IsWebAuthnSupported = function IsWebAuthnSupported() {
    if (!window.PublicKeyCredential) {
        console.log("Web Authentication API is not supported on this browser.");
        return false;
    }
    return true;
}

window.isWebAuthnPlatformAuthenticatorAvailable = function isWebAuthnPlatformAuthenticatorAvailable() {
    var timer;
    var p1 = new Promise(function(resolve) {
        timer = setTimeout(function() {
            console.log("isWebAuthnPlatformAuthenticatorAvailable - Timeout");
            resolve(false);
        }, 1000);
    });
    var p2 = new Promise(function(resolve) {
        if (IsWebAuthnSupported() && window.PublicKeyCredential.isUserVerifyingPlatformAuthenticatorAvailable) {
            resolve(
	            window.PublicKeyCredential.isUserVerifyingPlatformAuthenticatorAvailable().catch(function(err) {
                    console.log(err);
                    return false;
                }));
        }
        else {
            resolve(false);
        }
    });
    return Promise.race([p1, p2]).then(function (res) {
        clearTimeout(timer);
        console.log("isWebAuthnPlatformAuthenticatorAvailable - " +  res);
        return res;
    });
}

window.WebAuthnPlatformRegistration = function WebAuthnPlatformRegistration(publicKeyCredentialCreationOptions) {
    return new Promise(function(resolve, reject) {
        isWebAuthnPlatformAuthenticatorAvailable().then(function (result) {
            if (result) {
                resolve(Register(publicKeyCredentialCreationOptions));
            }
            reject(Error("UnSupportedBrowserError"));
        });
    });
}

function Register(publicKeyCredentialCreationOptions) {
    return new Promise(function(resolve, reject) {
        var options = JSON.parse(publicKeyCredentialCreationOptions);
        var publicKeyCredential = {};
        publicKeyCredential.rp = options.rp;
        publicKeyCredential.user = options.user;
        publicKeyCredential.user.id = new Uint8Array(options.user.id);
        publicKeyCredential.challenge = new Uint8Array(options.challenge);
        publicKeyCredential.pubKeyCredParams = options.pubKeyCredParams;
        // Optional parameters
        if ('timeout' in options) {
            publicKeyCredential.timeout = options.timeout;
        }
        if ('excludeCredentials' in options) {
            publicKeyCredential.excludeCredentials = credentialListConversion(options.excludeCredentials);
        }
        if ('authenticatorSelection' in options) {
            publicKeyCredential.authenticatorSelection = options.authenticatorSelection;
        }
        if ('attestation' in options) {
            publicKeyCredential.attestation = options.attestation;
        }
        if ('extensions' in options) {
            publicKeyCredential.extensions = options.extensions;
        }
        console.log(publicKeyCredential);
        navigator.credentials.create({"publicKey": publicKeyCredential, "signal": authAbortSignal})
            .then(function (newCredentialInfo) {
                // Send new credential info to server for verification and registration.
                console.log(newCredentialInfo);
                var publicKeyCredential = {};
                if ('id' in newCredentialInfo) {
                    publicKeyCredential.id = newCredentialInfo.id;
                }
                if ('type' in newCredentialInfo) {
                    publicKeyCredential.type = newCredentialInfo.type;
                }
                if ('rawId' in newCredentialInfo) {
                    publicKeyCredential.rawId = toBase64Str(newCredentialInfo.rawId);
                }
                if (!newCredentialInfo.response) {
                    throw "Missing 'response' attribute in credential response";
                }
                var response = {};
                response.clientDataJSON = toBase64Str(newCredentialInfo.response.clientDataJSON);
                response.attestationObject = toBase64Str(newCredentialInfo.response.attestationObject);
                publicKeyCredential.response = response;
                resolve(JSON.stringify(publicKeyCredential));
            }).catch(function (err) {
                // No acceptable authenticator or user refused consent. Handle appropriately.
                console.log(err);
                reject(Error(err.name));
        });
    });
}

function credentialListConversion(list) {
    var credList = [];
    for (var i=0; i < list.length; i++) {
        var cred = {
            type: list[i].type,
            id: new Uint8Array(list[i].id)
        };
        if (list[i].transports) {
            cred.transports = list[i].transports;
        }
        credList.push(cred);
    }
    return credList;
}

function toBase64Str(bin){
    return btoa(String.fromCharCode.apply(null, new Uint8Array(bin)));
}

```

## Step 4: Activate MFA device - FIDO2 Device

- Devices with a status of ACTIVATION_REQUIRED are activated with a valid attestation and origin. The attestation is generated by the browser as a response to a user action, such as a fingerprint or clicks on the FIDO2 device.

- The sample shows the POST /users/{{userID}}/devices/{{authId}} operation to activate the device specified in the request URL. This operation uses the application/vnd.pingidentity.device.activate+json custom content type in the request header to specify the activation action.

- The attestation property passes in the attestation JSON from the browser. The JSON looks like this:

<!--
type: tab
titles: Request, Response
-->

### Example of a attestation request 


```json
{
    "origin": "app.fiserv.com",
    "attestation": "{\"id\":\"ARacmDOuRE7DJV6L7w\",\"type\":\"public-key\",\"rawId\":\"ARacmDOuRE7DJV6L7w=\",\"response\":{\"clientDataJSON\":\"eyJ0eXBlIjoid2ViYXV0aG4uY3JlYXRYWxzZX0=\",\"attestationObject\":\"o2NmbXRmcGFja2VkZ2F0dFFO29h8n6WKBn6tHCQ=\"},\"clientExtensionResults\":{}}"
}
```

<!--
type: tab
-->

### Example of a validation (200: Created) response


```json
{
  "status": "SUCCESS",
  "message": "Device registered successfully"
}

```

<!-- type: tab-end --> 