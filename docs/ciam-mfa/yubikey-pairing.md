# MFA using YubiKey

A FIDO2 biometrics device such as Yubikey sflow uses functions from the Web Authentication API (webauthn API) to manage device registration (pairing) and authentication. The following sample JavaScript code will help you implement the webauthn API for browser-based operations.

## Step 1: Getting an access token     

Access tokens are credential strings that represent authorization to access a protected resource. Applications obtain access tokens by making OAuth 2 or OpenID Connect requests to an authorization server; MFA API resource servers require clients to authenticate using access tokens. Access tokens are obtained from the token endpoint (when using the client credentials grant type).

To get an access token, the following must be true:  

- The application is configured for MFA using  application onboarding process.

- The credentials are provided to application owner for getting an access token.  

- The application runtime  has access to the client secret and token endpoint. 


## Step 2: Create MFA  Device 

- API to Create MFA  deivce for user.

- As a pre-requisite user  must have a supported Yubikey hardware.

Attributes used in payload of request are as:

| Variable | Type | Required | Description |
| -------- | ---- | -------- | ----------- |
| `deviceType` | *string* | &#10004; | Fixed(SECURITY_KEY) |
| `deviceName` | *string* | - | Name of Yubikey device |
| `rp.id` | *string* | &#10004; | Your application URL prefix |
| `rp.name` | *string* | &#10004; | Application Name |

<!--
type: tab
titles: Request, Response
-->

**POST: /ciam-mfa/v2/users/{{user_name}}/mfadevices**

### Example of a Create MFA device 

```json
{
    "deviceType": "SECURITY_KEY",
    "deviceName": "Mydevice",
    "rp": {
        "id": "pingone.com",
        "name": "PingOne"
    },
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

Call the `navigator.credentials.create` method using the publicKeyCredentialOptions value returned from the Add  Device API:


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

## Step 4: Activate Security Key device

- Devices with a status of ACTIVATION_REQUIRED are activated with a valid attestation and origin. The attestation is generated by the browser as a response to a user action, such as a fingerprint or clicks on the security key.

- The sample shows the POST /users/{{userID}}/devices/{{authId}} operation to activate the device specified in the request URL. This operation uses the application/vnd.pingidentity.device.activate+json custom content type in the request header to specify the activation action.

- The attestation property passes in the attestation JSON from the browser. The JSON looks like this:

<!--
type: tab
titles: Request, Response
-->

### Example of a attestation request 


```json
{
    "origin": "https://app.pingone.com",
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
