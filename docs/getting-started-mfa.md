# What is Multi-Factor authentication (MFA)  

Multi-factor authentication (MFA) is an authentication method in which a computer user is granted access only after successfully presenting two or more pieces of evidence (or factors) to an authentication mechanism:  


- Knowledge (something the user and only the user knows)  

- Possession (something the user and only the user has)  

- Inherence (something the user and only the user is)  

By their nature, inherent factors are the strongest authentication factors and pose the lowest risk to security vulnerability.  

Fiserv Identity and access management  provides  simple and easy to integrate MFA  capabilities for enabling MFA actions in authentication flows. CIAM API gives you access to  most advance and secure authentication options.  

---  

## Registration 

- CIAM MFA API requires registration of application.

- Application team should submit a service point ticket to get yourself on-boarded.

- Service Catalog > Application Services > Customer IAM Application Registration

---

## CIAM MFA API  

CIAM MFA API provides MFA for the customer use case that protects Fiserv applications, and data resources. In a typical authentication flow:  

1. A user attempts to access a protected resource that is configured to use CIAM MFA, such as a gated website.  

2. The CIAM MFA API typically sends a notification on an out-of-band (OOB) channel to the users authentication device (possession factor), for further verification of the user�s identity. The notification to the user is communicated on a separate network channel, isolated from the network channel that the user used when entering their username and password. Use of an OOB channel enhances security, reducing the possibility of man-in-the-middle (MITM), phishing, and other security vulnerability attacks.  

3. CIAM MFA is configured to provide a one-time passcode (OTP) through SMS  or email notification, or Time-based One-Time Password (TOTP) authenticator app. The user must enter that passcode before it expires.  



## Integration use cases  

CIAM MFA has various configuration possibilities that allow application to determine their balance between security needs and demands for convenience (end-user experience). These options include the following:

<!-- type: row -->

<!-- type: card
title: MFA using SMS or Email
description: CIAM MFA API allows application to use Email ar SMS as authetnication factor.
link: ?path=docs/ciam-mfa/SMS-EMAIL.md
-->

<!-- type: card
title:  MFA using TOTP
description:  CIAM MFA API allows application to use Modern TOTP  authentication..
link: ?path=docs/ciam-mfa/TOTP.md
-->

<!-- type: row-end -->

<!-- type: row -->
<!-- type: card
title: MFA using Yubikey
description: Allows used to authenticate using hardware token device.
link: ?path=docs/ciam-mfa/yubikey.md
-->
<!-- type: card
title: MFA using FIDO2
description: Allows used to authenticate using registered FIDO2 device
link: ?path=docs/ciam-mfa/FIDO2/getting-started-FIDO2.md
-->
<!-- type: row-end -->
---

## Error Codes and messages

The below table contains the list of error codes and messages.

| Error Code | Error Message |
| ---------- | ------------- |
| `10001` | access token has been expired. |
| `10002` | Either access token is invalid or client is not registered. |
| `10003` | User not found please check the username. |
| `10004` | username must be unique. |
| `10005` | Validation Failed. |
| `10006` | No registered TOTP device found please register one. |
| `10006` | user found however no registered SECURITY_KEY device found for the user please register one. |
| `10006` | Device is already ACTIVE. |
| `10007` | please request a new otp. |
| `10007` | Invalid authId please try again. |
| `10008` | incorrect otp. |
| `10009` | otp must be six digit value. |
| `10010` | Template already exists. |
| `10010` | Device name already exists. |
| `10011` | Template not found. |
| `10012` | Error occurred while processing template please contact to the administrator. |
| `10014` | Maximum allowed devices has been reached for this account. |
| `10015` | Some error occurred please contact to the administrator. |
| `10026` | QUOTA_EXCEEDED Too many unsuccessful OTP attempts. |
| `10027` | PASSWORD_LOCKED_OUT Account is locked out. |
| `10028` | please provide: 'grant_type''client_id' and 'client_secret' under body: x-www-form-urlencoded to get the token. |
| `10029` | client credentials not allowed in Authorization: Basic Auth please provide: client credentials under body: x-www-form-urlencoded to get the token. |
| `10030` | please provide: 'client_id' - 'Key' and 'Value' under body: x-www-form-urlencoded to get the token. |
| `10031` | please provide: 'client_secret' - 'Key' and 'Value' under body: x-www-form-urlencoded to get the token. |
| `10050` | Device name not found. |
| `10051` | Device unpair failed. |
| `100001` | Phone Number is invalid. |
| `100016` | totp device not found please check the name. |
| `100016` | NO_USABLE_DEVICES No active totp device is available. |
| `100017` | please provide correct rpID no active FIDO device found for given rpId. |
| `100021` | Error while fetching detail. |
| `100025` | No FIDO device found please pair one. |
