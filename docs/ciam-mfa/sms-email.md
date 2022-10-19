# MFA using SMS or EMAIL 

- A user attempts to access a protected resource that is configured to use CIAM MFA, such as a gated website.  

- The CIAM MFA API  sends a notification on an out-of-band (OOB) channel to the user’s authentication device (possession factor), for further verification of the user’s identity.  

- The notification to the user is communicated on a separate network channel, isolated from the network channel that the user used when entering their username and password. Use of an OOB channel enhances security, reducing the possibility of man-in-the-middle (MITM), phishing, and other security vulnerability attacks.  

- CIAM MFA is configured to provide a one-time passcode (OTP) through SMS  or email notification, or Time-based One-Time Password (TOTP) authenticator app. The user must enter that passcode before it expires.

There are steps  required at the application-side that should meet the below criteria:  

- Can make http/REST calls  

- Has a user base that have either e-mail addresses, mobile phone for SMS or TOTP  


---  

- [Step 1: Getting an access token](#step-1-getting-an-access-token)  

- [Step 2: Request OTP](#step-2-request-otp)  

- [Step 3: Validate OTP](#step-3-validate-otp)  


---

## Step 1: Getting an access token     

Access tokens are credential strings that represent authorization to access a protected resource. Applications obtain access tokens by making OAuth 2 or OpenID Connect requests to an authorization server; MFA API resource servers require clients to authenticate using access tokens. Access tokens are obtained from the token endpoint (when using the client credentials grant type).

To get an access token, the following must be true:  

- The application is configured for MFA using  application onboarding process.

- The credentials are provided to application owner for getting an access token.  

- The application runtime  has access to the client secret and token endpoint.  


## Step 2: Request OTP 

The benefits of a encyrpted PIN Pad solution are:  

- All forms of electronic payment are accepted 

- Faster payment improving the customer experience 

- Business security by enabling acceptance of chip and signature, and chip and PIN 

<!--
type: tab
titles: Request, Response
-->

### Example of a request OTP  payload request using email 



```json
{
  "amount": {
    "total": "12.04",
    "currency": "USD"
  },
  "paymentSource": {
    "sourceType": "PaymentCard",
    "card": {
      "cardData": "4005550000000019",
      "expirationMonth": "02",
      "expirationYear": "2035",
      "securityCode": "123"
    }
  },
  "transactionDetails": {
    "captureFlag": true
  },
  "merchantDetails":{
      "merchantId": "123456789789567",
      "terminalId": "123456"
    }
}
```

## Step 3: Validate OTP 

The benefits of a encyrpted PIN Pad solution are:  

- Reduced coding effort for the developer because the encryption handling is already implemented by the third party vendor  

- All forms of electronic payment are accepted  

- Faster payment improving the customer experience  

<!--
type: tab
titles: Request, Response
-->

### Example of a charge payload request using `dynamicDescriptors`

```json
 {
   "amount":{
      "total": "12.04",
      "currency": "USD"
   },
   "source":{
      "sourceType": "PaymentCard",
      "card":{
         "cardData": "4005550000000019",
         "expirationMonth": "02",
         "expirationYear": "2035"
      }
   },
   "dynamicDescriptors":{
      "mcc": "4457",
      "merchantName": "Mywebsite.com",
      "customerServiceNumber": "1231231234",
      "serviceEntitlement": "67893827513",
      "address":{
         "street": "123 Main Street",
         "houseNumberOrName": "Unit B",
         "city": "Atlanta",
         "stateOrProvince": "GA",
         "postalCode": "30303",
         "country": "US"
      }
   },
   "transactionDetails":{
      "captureFlag": true
   },
   "merchantDetails":{
      "merchantId": "123456789789567",
      "terminalId": "123456"
   }
}
```

<!--
type: tab
-->

### Example of a charge (201: Created) response

<!-- theme: info -->
> See [Response Handling](?path=docs/Resources/Guides/Response-Codes/Response-Handling.md) for more information.

```json
{
   "gatewayResponse":{
      "orderId": "R-3b83fca8-2f9c-4364-86ae-12c91f1fcf16",
      "transactionType": "CHARGE",
      "transactionState": "AUTHORIZED",
      "transactionOrigin": "ECOM",
      "transactionProcessingDetails":{
         "transactionTimestamp": "2016-04-16T16:06:05Z",
         "apiTraceId": "rrt-0bd552c12342d3448-b-ea-1142-12938318-7",
         "clientRequestId": "30dd879c-ee2f-11db-8314-0800200c9a66",
         "transactionId": "838916029301"
      }
   },
   "source":{
      "sourceType": "PaymentCard",
      "card":{
         "cardData": "4005550000000019",
         "nameOnCard": "Jane Smith",
         "expirationMonth": "02",
         "expirationYear": "2035",
         "bin": "400555",
         "last4": "0019"
      }
   },
   "paymentReceipt":{
      "approvedAmount":{
         "total": 12.04,
         "currency": "USD"
      },
      "processorResponseDetails":{
         "approvalStatus": "APPROVED",
         "approvalCode": "OK3483",
         "authenticationResponseCode": "string",
         "referenceNumber": "845366457890-TODO",
         "schemeTransactionId": "019078743804756",
         "feeProgramIndicator": "123",
         "processor": "FISERV",
         "host": "NASHVILLE",
         "responseCode": "000",
         "responseMessage": "APPROVAL",
         "hostResponseCode": "00",
         "hostResponseMessage": "APPROVAL",
         "localTimestamp": "2016-04-16T16:06:05Z",
         "bankAssociationDetails":{
            "associationResponseCode": "000",
            "transactionTimestamp": "2016-04-16T16:06:05Z"
         }
      }
   },
   "dynamicDescriptors":{
      "mcc": "4457",
      "merchantName": "Mywebsite.com",
      "customerServiceNumber": "1231231234",
      "serviceEntitlement": "67893827513",
      "address":{
         "street": "123 Main Street",
         "houseNumberOrName": "Unit B",
         "city": "Atlanta",
         "stateOrProvince": "GA",
         "postalCode": "30303",
         "country": "US"
      }
   }
}
```

<!-- type: tab-end -->


---  

## See also  

- [API Explorer](./api/?type=post&path=/payments/v1/charges) 


---
