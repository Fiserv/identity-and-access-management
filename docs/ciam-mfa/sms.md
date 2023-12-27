# MFA using SMS 

- API to request MFA authentication through sms on mobile number. 

- The CIAM MFA API  sends a notification on an out-of-band (OOB) channel to the users authentication device (possession factor), for further verification of the users identity.  

- The notification to the user is communicated on a separate network channel, isolated from the network channel that the user used when entering their username and password. Use of an OOB channel enhances security, reducing the possibility of man-in-the-middle (MITM), phishing, and other security vulnerability attacks.  

- CIAM MFA is configured to provide a one-time passcode (OTP) through SMS notification. The user must enter that passcode before it expires.

There are steps  required at the application-side that should meet the below criteria:  

- Can make http/REST calls  

- Has a user base that have either e-mail addresses, mobile phone for SMS or TOTP  

Customization:  

- CIAM MFA API  allows to brand and customize notification template.  

- CIAM MFA API allows your application to send email from a trusted domain that you own

---  

- [Step 1: Getting an access token](#step-1-getting-an-access-token)  

- [Step 2: Request OTP](#step-2-request-otp)  

- [Step 3: Validate OTP](#step-3-validate-otp)  


---

## Step 1: Getting an access token     

Access tokens are credential strings that represent authorization to access a protected resource. Applications obtain access tokens by making OAuth 2 or OpenID Connect requests to an authorization server; MFA API resource servers require clients to authenticate using access tokens. Access tokens are obtained from the token endpoint (when using the client credentials grant type).

To get an access token, the following must be true:  

- The application is configured for MFA using  application registration process.

- The credentials are provided to application owner for getting an access token.  

- The application runtime  has access to the client secret and token endpoint.  


## Step 2: Request OTP 

API to initiate Second factor authentication by contacting the user using mobile number provided. 

- API will send one-time passcode to user device i.e. phone number. 

- API will return authId in response which will be required during device validation.  

- API supports custom templates that can be configured during application registration process. Custom template will allow to customize SMS messaging.

The payload parameters are as: 

| Variable | Type | Required | Description |
| -------- | -----| -------  | ----------- |
| `userName` | *string* | &#10004; | General Name |
| `phoneNumber` | *string* | &#10004; | Mobile number of the user |
| `deviceType` | *string* | &#10004; | sms(case insensitive) |

<!--
type: tab
titles: Request, Response
-->

Endpoint **:**

**POST** [{{base_url}}/ciam-mfa/v2/deviceAuthentications](../api/?type=post&path=/deviceAuthentications&version=2.0.0)

**Payload** **:**

```json
{
    "userName": "jdoe",
    "phoneNumber": "+91-8212345212",
    "deviceType": "sms"
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
    "message": "OTP has been sent to the device "
}
```

<!-- type: tab-end -->
## Step 3: Validate OTP 

API to validate one-time passcode that was sent on mobile number provided.

- API will authId in path and otp in the body to complete the validation.

- API will HTTP code, status and message in response to the validation process.

The payload parameters are as: 

| Variable | Type | Required | Description |
| -------- | -----| -------  | ----------- |
| `otp` | *string* | &#10004; | OTP received |
| `deviceType` | *string* | &#10004; | SMS(case insensitive) |

<!--
type: tab
titles: Request, Response
-->

Endpoint **:**

**POST** [{{base_url}}/ciam-mfa/v2/deviceAuthentications/{{authId}}](../api/?type=post&path=/deviceAuthentications/{authId}&version=2.0.0)

**Payload** **:**

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



