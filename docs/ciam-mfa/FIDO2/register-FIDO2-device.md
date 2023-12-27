## Register FIDO2 Device
FIDO2 registration flow is multistep process as depicted below.

---  

- [Step 1: Getting access token ](#step-1-getting-access-token)  

- [Step 2: Initiate device registration ](#step-2-initiate-device-registration)  

- [Step 3: Create a passkey (JavaScript WebAuthn API - Browser Side) ](#step-3-create-a-passkey-javascript-webauthn-api---browser-side)  

- [Step 4: Activate device ](#step-4-activate-device)

---

## Step 1: Getting access token      

Access tokens are credential strings that represent authorization to access a protected resource. Applications obtain access tokens by making OAuth 2 or OpenID Connect requests to an authorization server; MFA API resource servers require clients to authenticate using access tokens. Access tokens are obtained from the token endpoint (when using the client credentials grant type).

To get an access token, the following must be true:  

- The application is configured for MFA using  application registering process.

- The credentials are provided to application owner for getting an access token.  

- The application runtime  has access to the client secret and token endpoint. 


## Step 2: Initiate device registration 

- As a pre-requisite the FIDO2 service must be enabled for application.

- API requires user details, username and user email address along with relying party information.

- API will return "publicKeyCredentialCreationOptions" in response which will be required for browser side JavaScript WebAuthn API to consume and [create a passkey](#step-3-create-a-passkey-javascript-webauthn-api---browser-side)

- API will return "authId" in response which will be required during [device activation](#step-4-activate-device).

- Refer API explorer -> MFA -> Register Device for API reference. 



<!--
type: tab
titles: Request, Response
-->
Endpoint **:**

**POST** [{{base_url}}/ciam-mfa/v2/users/{{username}}/mfadevices](../api/?type=post&path=/users/{username}/mfadevices&version=2.0.0)

**Payload** **:**

```json
{
    "deviceType": "FIDO2",
    "rp": {
        "id": "app.fiserv.com",
        "name": "fiserv"
    },
    "email": "username@fiserv.com"
}
```

Attributes used in payload of request are as:

| Variable | Type | Required | Description |
| -------- | ---- | -------- | ----------- |
| `deviceType` | *string* | &#10004; | The type of device which user want to register for MFA. Note: irespective of device type user wants to register MOBILE/YUBIKY/PLATFORM for FIDO2 device registration fields value will always be "FIDO2". |
| `rp.id` | *string* | &#10004; | The ID of the relying party, used for logging in without having to provide a password. The value of the field should be a domain name, such as sample.com / fiserv.com |
| `rp.name` | *string* | &#10004; | The relying party's human-readable display name (for example, acme). |
| `email` | *string* | &#10004; | Email address of the user |

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
    "publicKeyCredentialCreationOptions": "{"rp":{"id":"app.fiserv.com","name":"fiserv"},"user":{"id":[-121,2,76,83,98,-86,-48,1,-114,31,-30,-9,116,52,-37,-78,68,-51,63,37,14,68,-112,56,-104,-7,-41,-116,-121,-46,-38,22],"displayName":"APM_NA_TEST_RUN_2102231126$demouser","name":"APM_NA_TEST_RUN_2102231126$demouser"},"challenge":[-19,41,45,-102,-21,109,-109,-125,32,121,-4,-78,-123,80,53,58,81,29,-111,81,75,11,-44,73,-81,90,4,42,-27,108,75,20],"pubKeyCredParams":[{"type":"public-key","alg":"-7"},{"type":"public-key","alg":"-37"},{"type":"public-key","alg":"-257"}],"timeout":120000,"excludeCredentials":[],"authenticatorSelection":{"residentKey":"required","requireResidentKey":true,"userVerification":"required"},"attestation":"none"}"
}

```
<!-- type: tab-end -->

## Step 3: Create a passkey (JavaScript WebAuthn API - Browser Side)

- Passwordless implmentation flow uses functions from the Web Authentication API (webauthn API) to manage device registration (pairing) and authentication.

- To create a passkey, browser side java script need to be executed. 

- Script requires input of "publicKeyCredentialCreationOptions" recevied in [initiate device registration](#step-2-initiate-device-registration).

- During script exceution browser will prompt user to choose available authenticator, request is been sent to the authenticator, user approves the request and authenticate himself, once user approves, passkey is been created.

- Once the passkey is generated on the device, an attestation object is created.

- Attestation object is required in [device activation](#step-4-activate-device).


**Note**: As a pre-requisite client browser should be compatible for FIDO2 (WebAuthn).

The following sample JavaScript code will help you implement the webauthn API for browser-based operations.

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

## Step 4: Activate device 

- Activate device is last step of registration. In this step user registration details get saved in server which is used to authenticate user later on.

- Once the passkey is created at step 3, an attestion object gets created by browser side script.

- Activate Device is an API call with below payload.

- *authId* recieved in initiate device registration.

- *attestation* created during create a passkey.

- *Origin* is name of the site from where the cilent is requesting.

- The attestation is the JSON object and the JSON looks like this:

<!--
type: tab
titles: Request, Response
-->

Endpoint **:**

**POST** [{{base_url}}/ciam-mfa/v2/users/{{username}}/mfadevices/{{authId}}](../api/?type=post&path=/users/{username}/mfadevices/{authId}&version=2.0.0)

**Payload** **:**

```json
{
    "origin": "https://app.fiserv.com",
    "attestation": "{\"id\":\"ARacmDOuRE7DJV6L7w\",\"type\":\"public-key\",\"rawId\":\"ARacmDOuRE7DJV6L7w=\",\"response\":{\"clientDataJSON\":\"eyJ0eXBlIjoid2ViYXV0aG4uY3JlYXRYWxzZX0=\",\"attestationObject\":\"o2NmbXRmcGFja2VkZ2F0dFFO29h8n6WKBn6tHCQ=\"},\"clientExtensionResults\":{}}"
}
```

Attributes used in payload of request are as:

| Variable | Type | Required | Description |
| -------- | ---- | -------- | ----------- |
| `origin` | *string* | &#10004; | App origin |
| `attestation` | *string* | &#10004; | Object |


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