# TOTP Device Resgistration 

TOTP stands for Time-based One-Time Passwords and is a common form of two factor authentication (2FA). Unique numeric passwords are generated with a standardized algorithm that uses the current time as an input. The time-based passwords are available offline and provide user friendly, increased account security when used as a second factor.

TOTP 2FA benefits - 

- Offline support

- PII-less registration 

- Standardized authentication solution 

- Software based, not dependent on carrier fees or telephony access and deliverability 

- Faster average time to authenticate

---  

To Verify user using TOTP, first step required is to  register Time-based One-time Password (TOTP) authenticator resource.

- [Step 1: Getting an access token](#step-1-getting-an-access-token)  

- [Step 2: Create TOTP Device](#step-2-create-totp-device)  

- [Step 3: Device pairing] (# step-3-device-pairing)

- [Step 3: Register TOTP device](#step-4-register-totp-device)  


---

## Step 1: Getting an access token     

Access tokens are credential strings that represent authorization to access a protected resource. Applications obtain access tokens by making OAuth 2 or OpenID Connect requests to an authorization server; MFA API resource servers require clients to authenticate using access tokens. Access tokens are obtained from the token endpoint (when using the client credentials grant type).

To get an access token, the following must be true:  

- The application is configured for MFA using  application onboarding process.

- The credentials are provided to application owner for getting an access token.  

- The application runtime  has access to the client secret and token endpoint.  


## Step 2: Create TOTP Device 

- API to Create TOTP  deivce for user.

- As a pre-requisite user  must install a supported authenticator app on the mobile device they  intend to register for MFA.

- Each user must enable MFA for themselves using a device they will have access to every time they sign in. An administrator cannot enable MFA for another user.

- API will return secret and registration URL in response that will be used for device paring.


<!--
type: tab
titles: Request, Response
-->

### Example of a request OTP  payload request using email 

```json
{
    "deviceType": "TOTP",
    "deviceName": "Mydevice",
}
```
<!--
type: tab
-->

### Example of authentication request (201: Created) response

<!-- theme: info -->
> See [Response Handling](?path=docs/Resources/Guides/Response-Codes/Response-Handling.md) for more information.

```json
{
    "authId": "0063f27c-787b-4046-8b8e-a75e241b5ea6",
    "status": "SUCCESS",
    "message": "Please get the OTP from registered device to authenticate "
}
```

<!-- type: tab-end -->


## Step 3: Device pairing

- Application should create a QR code that will be geenrated using registration URI and secret returned by API in response.

- The QR code shares a secret key with the authenticator app to enable the app to generate TOTPs that can be verified by the CIAM API  service.

- To enable MFA, user should their  mobile device's authenticator app to scan generated  QR code that is generated using regsitration URI and secret returned by the CIAM API. 


## Step 3: Register TOTP device 

- API to complete device registration process.

- After sucessfull  paring device activation is required for completing sevice registration.

- Authenticator app will device a code after pairing that will be sent in request for activation.

- API will require authId in path that was sent in the response of add device request and otp in the body to complete the validation.

- API will HTTP code,  status and message in response to the validation process. 

<!--
type: tab
titles: Request, Response
-->

### Example of a validation request

```json
 {
  "otp": "523471"
}
```

<!--
type: tab
-->

### Example of a validation (200: Created) response

<!-- theme: info -->
> See [Response Handling](?path=docs/Resources/Guides/Response-Codes/Response-Handling.md) for more information.

```json
{
  "status": "SUCCESS",
  "message": "OTP has been validated successfully"
}

```

<!-- type: tab-end -->


---  

## See also  

- [API Explorer](./api/?type=post&path=/payments/v1/charges) 


---
