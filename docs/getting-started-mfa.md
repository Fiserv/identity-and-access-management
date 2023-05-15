# What is Multi-Factor authentication (MFA)  

Multi-factor authentication (MFA) is an authentication method in which a computer user is granted access only after successfully presenting two or more pieces of evidence (or factors) to an authentication mechanism:  


- Knowledge (something the user and only the user knows)  

- Possession (something the user and only the user has)  

- Inherence (something the user and only the user is)  

By their nature, inherent factors are the strongest authentication factors and pose the lowest risk to security vulnerability.  

Fiserv Identity and access management  provides  simple and easy to integrate MFA  capabilities for enabling MFA actions in authentication flows. CIAM API gives you access to  most advance and secure authentication options.  

---  

## Onboarding 

- CIAM MFA API requires registration of application.

- Application team should submit a service point ticket to get yourself on-boarded.

- Service Catalog > Application Services > Customer IAM Application Onboarding

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
link: ?path=docs/ciam-mfa/sms-email.md
-->

<!-- type: card
title:  MFA using TOTP
description:  CIAM MFA API allows application to use Modern TOTP  authentication..
link: ?path=docs/ciam-mfa/TOTP.md
-->

<!-- type: card
title: MFA using Yubikey
description: Allows used to authenticate using hardware token device.
link: ?path=docs/ciam-mfa/yubikey.md
-->

<!-- type: row-end -->

---
