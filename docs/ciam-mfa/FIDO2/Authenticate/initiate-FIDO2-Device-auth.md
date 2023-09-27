## Authenticate FIDO2 Device

FIDO2 authentication flow uses functions from the Web Authentication API (webauthn API) for FIDO2 device  authentication. The following sample JavaScript code will help you implement the webauthn API for browser-based operations.

---  

- [Step 1: Getting an access token](#step-1-getting-an-access-token)  

- [Step 2: Initialize authentication](#step-2-initiate-device-authentication---fido2-device)  

- [Step 3: Device Pairing](#step-3-device-pairing)  

- [Step 4: Validate assertion](#step-4-validate-assertion)

---

## Step 1: Getting an access token     

Access tokens are credential strings that represent authorization to access a protected resource. Applications obtain access tokens by making OAuth 2 or OpenID Connect requests to an authorization server; MFA API resource servers require clients to authenticate using access tokens. Access tokens are obtained from the token endpoint (when using the client credentials grant type).

To get an access token, the following must be true:  

- The application is configured for MFA using  application onboarding process.

- The credentials are provided to application owner for getting an access token.  

- The application runtime  has access to the client secret and token endpoint. 


## Step 2: Initiate Device Authentication - FIDO2 Device 

- API will initiate  device authentication and return authId in response which will be required during  validation.  

<!--
type: tab
titles: Request, Response
-->

### Example of a Inititate Device Authentication

```json
{
	"userName":"username",
    "rpID": "app.fiserv.com",
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
    "publicKeyCredentialRequestOptions": "{"challenge":[13,93,-97,-86,-108,28,22,-98,-9,-53,37,23,-105,-122,-64,-75,57,-88,-13,57,-112,96,-33,42,-119,-72,116,-94,95,-50,-42,99],"timeout":120000,"rpId":"iam-demo.1dc.com","allowCredentials":[{"type":"public-key","id":[-114,11,-40,2,-85,-109,-107,-126,-25,-5,-80,113,-9,-25,-24,-98,123,27,-25,-34,6,-66,65,-8,60,-88,-56,16,-78,88,-57,-29,0,-93,23,-50,61,-11,-31,-128,-62,-14,-43,-59,-52,33,-110,-127,-60,31,-26,36,-45,77,64,94,-83,56,3,87,-122,-31,94,-107]}],"userVerification":"preferred"}"
}


```

<!-- type: tab-end -->


## Step 3: Execute browser side JavaScript - webauthn API

 FIDO2 device authentication flow uses functions from the Web Authentication API (webauthn API) to manage device authentication. The following sample JavaScript code will help you implement the webauthn API for browser-based operations.

Call the navigator.credentials.get method using the publicKeyCredentialOptions returned from the assertion.check

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

window.WebAuthnPlatformAuthentication = function WebAuthnPlatformAuthentication(publicKeyCredentialRequestOptions) {
    return new Promise(function(resolve, reject) {
        isWebAuthnPlatformAuthenticatorAvailable().then(function (result) {
            if (result) {
                resolve(Authenticate(publicKeyCredentialRequestOptions));
            }
            reject(Error("UnSupportedBrowserError"));
        });
    });
}

function Authenticate(publicKeyCredentialRequestOptions) {
    return new Promise(function(resolve, reject) {
        var options = JSON.parse(publicKeyCredentialRequestOptions);
        var publicKeyCredential = {};
        publicKeyCredential.challenge = new Uint8Array(options.challenge);
        if ('allowCredentials' in options) {
            publicKeyCredential.allowCredentials = credentialListConversion(options.allowCredentials);
        }
        if ('rpId' in options) {
            publicKeyCredential.rpId = options.rpId;
        }
        if ('timeout' in options) {
            publicKeyCredential.timeout = options.timeout;
        }
        if ('userVerification' in options) {
            publicKeyCredential.userVerification = options.userVerification;
        }
        console.log(publicKeyCredential);
        navigator.credentials.get({"publicKey": publicKeyCredential})
            .then(function (assertion) {
                // Send new credential info to server for verification and registration.
                console.log(assertion);
                var publicKeyCredential = {};
                if ('id' in assertion) {
                    publicKeyCredential.id = assertion.id;
                }
                if ('rawId' in assertion) {
                    publicKeyCredential.rawId = toBase64Str(assertion.rawId);
                }
                if ('type' in assertion) {
                    publicKeyCredential.type = assertion.type;
                }
                var response = {};
                response.clientDataJSON = toBase64Str(assertion.response.clientDataJSON);
                response.authenticatorData = toBase64Str(assertion.response.authenticatorData);
                response.signature = toBase64Str(assertion.response.signature);
                response.userHandle = toBase64Str(assertion.response.userHandle);
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

const isWebAuthnSupported = () => {
  if (!window.PublicKeyCredential) {
    return false;
  }
  return true;
};

function getCompatibility() {
  return isWebAuthnPlatformAuthenticatorAvailable()
      .then((result) => {
        if (result) {
          return 'FULL';
        } else if (isWebAuthnSupported()) {
          return 'FIDO2_ONLY';
        } else {
          return 'NONE';
        }
      })
      .catch(() => {
        if (isWebAuthnSupported()) {
          return 'FIDO2_ONLY';
        } else {
          return 'NONE';
        }
      });
}

```

## Step 4: Authenticate FIDO2 Device

- The multi-factor authentication flow for FIDO2 device checks the authenticator assertion response, which contains the signed challenge needed to complete the MFA flow. The MFA actions service validates the challenge.

- The following sample shows the operation to validate the assertion used in the multi-factor authentication flow. 

<!--
type: tab
titles: Request, Response
-->

### Example of a check assertion request 


```json
{
    "origin": "app.fiserv.com",
    "assertion": "{{assertionFromBrowser}}"
}
    
```

<!--
type: tab
-->

### Example of a validation (200: Created) response


```json
{
  "status": "SUCCESS",
  "message": "Authentication completed succesfully"
}

```

<!-- type: tab-end --> 


Initiates an MFA device authentication flow.
<!--
type: tab
titles: Request, Response
-->

Attributes used in Payload of request are as:

| Variable | Type | Required | Description |
| -------- | ---- | -------- | ----------- |
| `rpID` | *string* | &#10004; | The ID of the relying party. The value should be a domain name, such as example.com |


