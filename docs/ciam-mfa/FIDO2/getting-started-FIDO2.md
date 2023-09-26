# MFA using FIDO2

* CIAM MFA API allows you to use FIDO2 device to access/login your account without password, with the added security of multi-factor authentication.

* FIDO2 is the term for a Passworldless authentication open standard developed by the Fast Identity Online (FIDO) Alliance.

* FIDO2 enable users to simply sign in with passkeys using their devices with a biometric or a security key.

* FIDO2 authentication is a multi-step process where device registration as a pre-requisite, before it can be used for passwordless login, refer below information for device registration and authentication.


<!-- type: row -->

<!-- type: card
title: Register FIDO2 Device
description: Registering Device for FIDO2 authentication
link: ?path=docs/ciam-mfa/FIDO2/Register/register-FIDO2-device.md
-->

<!-- type: card
title:  FIDO2 Authentication
description: Authentication usign FIDO2
link: ?path=docs/ciam-mfa/Authenticate/initiate-FIDO2-Device-auth.md
-->

<!-- type: row-end -->

## FIDO2 Devices

In FIDO2 authentication, users use FIDO2 devices to authenticate themselves.
	
FIDO2 devices are divided into two categories as below.

* **Platform Devices**, its same device from where user is trying to login. To authenticate with a platform authenticator, device should be capable of taking user biometrics. Some examples are MacBook’s Touch Bar, Windows Hello, iOS Touch/FaceId, and Android’s fingerprint/face recognition.
	
* **Roaming Devices** are removable and cross-platform, like a YubiKey, Mobile and can be used on multiple devices. To authenticate with a roaming authenticator, you need to connect it to the device (through USB, NFC, or Bluetooth), provide proof of presence (by touching it, for example), and optionally provide user verification, for example, by entering a PIN.

**Note**: FIDO2 devices are also referred to as authenticators.

## How does FIDO2 work?
User need to register the device once and use that device every time for login.

#### Device Registration
**Step 1**: During account registration, the user is prompted to choose available authenticator.
[ Fiserv application will use CIAM MFA FIDO2 API to initiate the device registration process.]

**Step 2**: Request sent to the authenticator.

**Step 3**: User approves the request and authenticate himself by performing an action on authenticator, common actions include touching a fingerprint reader, touching a security key, entering a PIN, or other approved authentication methods.

**Step 4**: Once user approves, a public/private key(passkey) pair is created that is unique to the user’s device(authenticator), the user’s account, and the application.

**Step 5**: The public key is sent to the Fiserv application and associated with the user’s account. The public key is sent to the Fiserv application in the form of attestation object.
[ Fiserv application will use CIAM MFA API to store attestation object. ] 

**Step 6**: The private key(passkey) is stored in user’s device(authenticator) and never leaves the user’s device.

#### Login/Authentication

**Step 1**: During Login, the user is prompted to choose authenticator.
[ Fiserv application will make use of CIAM MFA here for initiating the authentication. ]

**Step 2**: User needs to choose authenticator used during registration.

**Step 3**: Request sent to the respective authenticator.

**Step 4**: User approves the request and authenticate himself by performing an same action that they performed during the registration process on authenticator. like touching a fingerprint reader, touching a security key, entering a PIN, or other approved authentication methods.

**Step 5**: Once user approves, the device/authenticator looks up the private key(Passkey) based on the ID provided by the application and generates the assertion object and sends it back to the application for verification.

**Step 6**: The application verifies the assertion object using CIAM MFA FIDO2 API.
[ Fiserv application will use CIAM MFA API here for validating the assertion object ]

**Step 7**: The user is logged in if assertion object is verified successfully by CIAM MFA FIDO2 API.

## What are Passkeys?
Passkeys are a replacement for passwords. Passkeys are a safer and easier alternative to passwords. With passkeys, users can sign in to apps and websites with a biometric sensor (such as a fingerprint or facial recognition), PIN, or pattern, freeing them from having to remember and manage passwords.                                

## Why FIDO2 Authentication?

•	Security
    FIDO2 passkey are proven to be resistant to threats of phishing, credential stuffing and other remote attacks. FIDO2 more secure than passwords and SMS OTPs.

•	Privacy
    FIDO2 passkeys are unique for each internet site, they cannot be used to track users across sites. Plus, biometric data, when used, never leaves the user’s device.

•	Convenience
    The user experience will be simple verification of their fingerprint or face, or a device PIN. User can select the device that best fits their needs.
