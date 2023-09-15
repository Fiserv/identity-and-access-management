# MFA using FIDO2

CIAM MFA supports the use of the FIDO2 biometrics and FIDO2 security keys for authentication.

Users can authenticate with FIDO2 security keys or FIDO2-compatible accessing devices by using a gesture that is enabled by built-in biometrics support on the devices.

CIAM MFA’s FIDO2 compliance provides security benefits, including protection against phishing, man-in-the-middle, and replay attacks. This includes the following FIDO2 protocol security measures:

	* Based on public key cryptography

	* Ensures that private keys remain on the FIDO2 device only

	* Does not employ server-side shared secrets, that could otherwise be compromised

	* Isolates services from accounts
    
	* Does not employ a third party in the FIDO2 protocol