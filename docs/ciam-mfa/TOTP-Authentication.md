# MFA using TOTP Device


---  

- [Step 1: Getting an access token](#step-1-getting-an-access-token)  

- [Step 2: Initialize authentication](#step-2-initialize-authentication)  

- [Step 3: Validate OTP](#step-3-validate-otp)  


---

## Step 1: Getting an access token     

Access tokens are credential strings that represent authorization to access a protected resource. Applications obtain access tokens by making OAuth 2 or OpenID Connect requests to an authorization server; MFA API resource servers require clients to authenticate using access tokens. Access tokens are obtained from the token endpoint (when using the client credentials grant type).

To get an access token, the following must be true:  

- The application is configured for MFA using  application onboarding process.

- The credentials are provided to application owner for getting an access token.  

- The application runtime  has access to the client secret and token endpoint.  


## Step 2: Initialize  authentication 

API will initalize TOTP device authentication return authId in response which will be required during OTP validation.  



<!--
type: tab
titles: Request, Response
-->

### Example of a request OTP  payload request using email 



```json
{
	"userName":"demouser",
    "deviceName": "mydevice",
    "deviceType": "TOTP"
}
```
<!--
type: tab
-->

### Example of authentication request (201: Created) response

```json
{
    "authId": "0063f27c-787b-4046-8b8e-a75e241b5ea6",
    "status": "SUCCESS",
    "message": "Please get the OTP from registered device to authenticate"
}
```

<!-- type: tab-end -->
## Step 3: Validate OTP 

- API will authId in path and otp in the body to complete the validation.

- API will HTTP code ,  status and message in response to the validation process.

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


```json
{
  "status": "SUCCESS",
  "message": "OTP has been validated successfully"
}

```

<!-- type: tab-end -->



