# MFA using YubiKey

---  

- [Step 1: Getting an access token](#step-1-getting-an-access-token)  

- [Step 2: Initialize authentication](#step-2-initialize-authentication)  

- [Step 3: Validate OTP](#step-3-validate-otp)  


---

A FIDO2 biometrics device such as Yubikey sflow uses functions from the Web Authentication API (webauthn API) to manage device registration (pairing) and authentication. The following sample JavaScript code will help you implement the webauthn API for browser-based operations.

## Step 1: Getting an access token     

Access tokens are credential strings that represent authorization to access a protected resource. Applications obtain access tokens by making OAuth 2 or OpenID Connect requests to an authorization server; MFA API resource servers require clients to authenticate using access tokens. Access tokens are obtained from the token endpoint (when using the client credentials grant type).

To get an access token, the following must be true:  

- The application is configured for MFA using  application onboarding process.

- The credentials are provided to application owner for getting an access token.  

- The application runtime  has access to the client secret and token endpoint. 


## Step 2: Create MFA  Device 

- API will initiate  device authentication and return authId in response which will be required during  validation.  

The payload parameters are as: 

| Variable | Type | Required | Description |
| -------- | -----| -------  | ----------- |
| `userName` | *string* | &#10004; | General Name |
| `deviceName` | *string* | &#10004; | Name of the device |
| `deviceType` | *string* | &#10004; | Fixed(SECURITY_KEY) |

<!--
type: tab
titles: Request, Response
-->

### Example of a Create MFA device 

```json
{
    "deviceType": "SECURITY_KEY",
    "deviceName": "Mydevice",
    "userName":"demouser"   
}
```
<!--
type: tab
-->

### Example of authentication request (201: Created) response


```json
{
    "authId": "09859da1-aed0-4be0-af1d-5583471b5d9c",
    "deviceType": "SECURITY_KEY",
    "status": "ACTIVATION_REQUIRED",
    "message": "Device registration has been initiated, please activate the device to use"
    "deviceName": "Mydevice",
    "rp": {
        "id": "pingone.com",
        "name": "pingone.com"
    },
    "publicKeyCredentialCreationOptions": "{\"rp\":{\"id\":\"pingone.com\"},\"user\":{\"id\":[-80,-62,-62,-66,84,85,-36,51,81,8,95,88,-105,64,103,-72,14,-18,-24,54,65,-58,-79,36,10,-55,-93,33,108,41,37,-94],\"displayName\":\"9ad15e9e-3ac6-43f7-a053-d46b87d6c4a7_tomjones\",\"name\":\"9ad15e9e-3ac6-43f7-a053-d46b87d6c4a7_tomjones\"},\"challenge\":[-103,5,109,97,69,75,87,108,-122,-11,54,15,-111,-60,-32,-92,-91,-21,70,34,96,-72,87,66,-45,-5,-99,-112,26,110,-33,-112],\"pubKeyCredParams\":[{\"type\":\"public-key\",\"alg\":\"-7\"},{\"type\":\"public-key\",\"alg\":\"-37\"},{\"type\":\"public-key\",\"alg\":\"-257\"}],\"timeout\":120000,\"excludeCredentials\":[],\"authenticatorSelection\":{\"authenticatorAttachment\":\"cross-platform\",\"requireResidentKey\":false,\"userVerification\":\"preferred\"},\"attestation\":\"direct\"}"
}


```

<!-- type: tab-end -->


## Step 3: Device pairing

A  Yubikey device flow uses functions from the Web Authentication API (webauthn API) to manage device authentication. The following sample JavaScript code will help you implement the webauthn API for browser-based operations.

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
          return 'SECURITY_KEY_ONLY';
        } else {
          return 'NONE';
        }
      })
      .catch(() => {
        if (isWebAuthnSupported()) {
          return 'SECURITY_KEY_ONLY';
        } else {
          return 'NONE';
        }
      });
}

```

## Step 4: Validating  Security Key device

- The multi-factor authentication flow for a Yubikey device checks the authenticator assertion response, which contains the signed challenge needed to complete the MFA flow. The MFA actions service validates the challenge.

- The following sample shows the operation to validate the assertion used in the multi-factor authentication flow. 

- This operation uses the application/vnd.pingidentity.assertion.check+json custom media type as the content type in the request header.

Attributes used in payload of request are as:

| Variable | Type | Required | Description |
| -------- | ---- | -------- | ----------- |
| `origin` | *string* | &#10004; | App origin |
| `attestation` | *string* | &#10004; | Object |

<!--
type: tab
titles: Request, Response
-->

**POST /ciam-mfa/v2/deviceAuthentications/{{authId}}**

### Example of a check assertion request 


```json
{
    "origin": "https://app.pingone.com",
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
