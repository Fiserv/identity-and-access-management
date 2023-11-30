## Authenticate FIDO2 Device - usernameless
FIDO2 authentication flow is multistep process as depicted below.

---  

- [Step 1: Getting an access token](#step-1-getting-an-access-token)  

- [Step 2: Initiate device authentication usernameless](#step-2-initiate-device-authentication-usernameless)  

- [Step 3: Validate user (JavaScript WebAuthn API - Browser Side)](#step-3-validate-user-javascript-webauthn-api---browser-side)  

- [Step 4: Validate assertion](#step-4-validate-assertion)

---

## Step 1: Getting an access token     

Access tokens are credential strings that represent authorization to access a protected resource. Applications obtain access tokens by making OAuth 2 or OpenID Connect requests to an authorization server; MFA API resource servers require clients to authenticate using access tokens. Access tokens are obtained from the token endpoint (when using the client credentials grant type).

To get an access token, the following must be true:  

- The application is configured for MFA using  application onboarding process.

- The credentials are provided to application owner for getting an access token.  

- The application runtime  has access to the client secret and token endpoint. 


## Step 2: Initiate Device Authentication Usernameless

- API will initiate  device authentication and return authId in response which will be required during assertion validation.  

- As a pre-requisite the FIDO2 service must be enabled for application.

- API requires username, rpID and deviceType as request payload.

- API will return *publicKeyCredentialCreationOptions* in response which will be required for browser side JavaScript WebAuthn API to consume and [create a passkey](#step-3-validate-user-javascript-webauthn-api---browser-side )

- API will return *authId* in response which will be required during [validate assertion](#step-4-validate-assertion).

- Refer API explorer -> MFA -> Authenticate FIDO2 Device.

<!--
type: tab
titles: Request, Response
-->
Endpoint to inititate device authentication **:**

**POST /ciam-mfa/v2/users/deviceAuthentications**

Payload to inititate device authentication **:**

```json
{
    "rpID": "https://app.fiserv.com",
    "deviceType": "FIDO2"
}
```

Attributes used in payload of request are as:

| Variable | Type | Required | Description |
| -------- | ---- | -------- | ----------- |
| `userName` | *string* | &#10004; | userName |
| `rpID` | *string* | &#10004; | URL |
| `deviceType` | *string* | &#10004; | Authentication Device |

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


## Step 3: Validate User (JavaScript WebAuthn API - Browser Side)

- Passwordless implmentation flow uses functions from the Web Authentication API (webauthn API) to manage FIDO2 device authentication.

- To validate user(ask for user biometrics to validate), browser side java script need to be executed. 

- Script requires input of "publicKeyCredentialCreationOptions" recevied in [initiate device authentication](#step-2-initiate-device-authentication).

- During script exceution browser will prompt user to choose available authenticator, request is been sent to the authenticator, user authenticate themself by providing the biometrics.

- Once the user is authenticated successfully, an assertion object is created by the browser side script.

- Assertion object is required during [Validate Assertion](#step-4-validate-assertion).


**Note**: As a pre-requisite client browser should be compatible for FIDO2 (WebAuthn).

Differnece: In usernamless flow, autheticator like mobile will showcase the list of all the accounts whose passkeys are stored for given rpID and user need to select one apropriate account followed by providind biometrics to generate assertion with right userHandle.

For authticator like security key or platform no account selection required just providing biometrics will genrate assertion with the right userHandle.

Note: With the help of "userHandle" server identifies which user's authetication request is this. 


The following sample JavaScript code will help you implement the webauthn API for browser-based operations.

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

## Step 4: Validate assertion

- Validate assertion is last step of authentication. In this step assertion gets validated with server to verify if the same registered user is trying to login.

- Once the user is validated at step 3, an assertion object gets created by browser side script.

- Validation assertion is an API call with below payload.

- *authId* recieved in initiate device authentication.

- *assertion* created during create a passkey step.

- *Origin* is name of the site from where the cilent is requesting.

- The assertion is the JSON object and the JSON looks like this:

**Note**: In usernamless flow assertion object has "userHandle" value which tells server which user is requesting for authetication
<!--
type: tab
titles: Request, Response
-->

Endpoint for  validate assertion **:**

**POST /ciam-mfa/v2/users/deviceAuthentications/{authId}**

Payload for validate assertion - usernameless **:**


```json
{
    "deviceType": "FIDO2",
    "origin": "https://app.fiserv.com",
    "assertion": "{\"id\":\"j6I9tovjxsVtndQQZJ43rQ\",\"rawId\":\"j6I9tovjxsVtndQQZJ43rQ==\",\"type\":\"public-key\",\"response\":{\"clientDataJSON\":\"eyJ0eXBlIjoid2ViYXV0aG4uZ2V0IiwiY2hhbGxlbmdlIjoiU2NmbktzSmNWNnR4WXBrWTd4bW5Yd3BQeXJRYTZ0SlJxVENmak9uN1hzUSIsIm9yaWdpbiI6Imh0dHBzOi8vbG9jYWxob3N0Ojk0NDMiLCJjcm9zc09yaWdpbiI6ZmFsc2V9\",\"authenticatorData\":\"SZYN5YgOjGh0NBcPZHZgW4/krrmihjLHmVzzuoMdl2MdAAAAAA==\",\"signature\":\"MEUCIQD8miXpRynxQ+cV9utI7E2Cs/mS47IagF2RqbfKK+DMlAIgWNS6sJA0R4NoNBt+aW1Z9NZGm7hUQDMyw6GwNYFBRQc=\",\"userHandle\":\"ey2q99IUCnLDfygPtwwrvhr7q/XycIe1IjgMXDKildk=\"}}"
}
    
```
| Variable | Type | Required | Description |
| -------- | ---- | -------- | ----------- |
| `deviceType` | *string* | &#10004; | Authentication Device |
| `origin` | *string* | &#10004; | URL |
| `assertion` | *string* | &#10004; | assertion object |

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

