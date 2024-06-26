# TOTP Device Registration 

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

- [Step 3: Device pairing](#step-3-device-pairing)

- [Step 4: Activate Device](#step-4-activate-device)  


---

## Step 1: Getting an access token     

Access tokens are credential strings that represent authorization to access a protected resource. Applications obtain access tokens by making OAuth 2 or OpenID Connect requests to an authorization server; MFA API resource servers require clients to authenticate using access tokens. Access tokens are obtained from the token endpoint (when using the client credentials grant type).

To get an access token, the following must be true:  

- The application is configured for MFA using  application registration process.

- The credentials are provided to application owner for getting an access token.  

- The application runtime  has access to the client secret and token endpoint.  


## Step 2: Create TOTP Device 

- API to Create TOTP  device for user.

- As a pre-requisite user  must install a supported authenticator app on the mobile device they  intend to register for MFA.

- Each user must enable MFA using the device they will have access to everytime. An administrator cannot enable MFA for another user.

- API will return secret and registration URL in response that will be used for device paring.


<!--
type: tab
titles: Request, Response
-->

Endpoint **:**

**POST** [{{base_url}}/users/{username}/mfadevices](../api/?type=post&path=/users/{username}/mfadevices&version=2.0.0)

**Payload** **:** 

```json
{
    "deviceType": "TOTP",
    "deviceName": "iphone6",
}
```
<!--
type: tab
-->

### Example of authentication request (201: Created) response


```json
{
    "authId": "c0b26a2e-6142-4640-9dd7-1ebd488d46f5",
    "deviceType": "TOTP",
    "status": "ACTIVATION_REQUIRED",
    "message": "Device registration has been initiated, please activate the device to use",
    "deviceName": "iphone6",
    "secret": "LXXXWKFKAKKIGOSP62SORVM67GECU6P2",
    "registrationUri": "otpauth://totp/APM0000003$jdoe?secret=LXXXWKFKAKKIGOSP62SORVM67GECU6P2"
}
```

<!-- type: tab-end -->


## Step 3: Device pairing

- Device parining is  required for  sharing of secret key with  with the authenticator app to enable the app to generate TOTPs that can be verified by the CIAM API  service.

- Two options are available for Device pairing

- **Option:1** requires application to provide user with the enter secret key that was  within Step-2 response. To enable MFA, user should key in secret key  manually and attach it to authenticator application.

- **Option:2** provides a better user experience where application should create a QR code using registration URI returned within  Step-2  API  response. To enable MFA, user should use their  mobile devices authenticator app to scan generated  QR code. 


## Step 4: Activate Device 

- API to complete device registration process.

- After successfull paring device activation is required for completing sevice registration.

- Authenticator app will send a code after pairing. That code should be passed in request payload for activation.

- API will require authId in path that was sent in the response of add device request and otp in the body to complete the validation.

- API will return HTTP code,  status and message in response to the validation process. 

The payload parameters are as: 

| Variable | Type | Required | Description |
| -------- | -----| -------  | ----------- |
| `DeviceType` | *string* | &#10004; | TOTP(case insensitive) |
| `OTP` | *string* | &#10004; | The OTP sent on TOTP device |

<!--
type: tab
titles: Request, Response
-->

Endpoint **:**

**POST** [{{base_url}}/users/{username}/mfadevices/{authId}](../api/?type=post&path=/deviceAuthentications/{authId}&version=2.0.0)

**Payload** **:**

```json
{
  "deviceType":"TOTP",
  "otp": "523471"
}
```

<!--
type: tab
-->

### Example of a validation (200: Success) response


```json
{
  "status": "ACTIVE",
  "message": "iphone6"
}

```

<!-- type: tab-end -->


