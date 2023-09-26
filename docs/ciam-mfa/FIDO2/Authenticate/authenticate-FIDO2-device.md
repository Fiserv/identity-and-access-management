## Authenticate FIDO2 Device

This api is used to validate the assertion used in the multi-factor authentication flow. This operation uses the application/vnd.pingidentity.assertion.check+json custom media type as the content type in the request header.

<!--
type: tab
titles: Request, Response
-->

Attributes in Payload of request are as:

| Variable | Type | Required | Description |
| -------- | ---- | -------- | ----------- |
| `origin` | *string* | &#10004; | The originating server (for example, https://apps.pingone.com). This property and the attestation property are used to activate FIDO2 devices that have a status of ACTIVATION_REQUIRED. This is a required property for FIDO2 device activation. |
| `assertion` | *string* | &#10004; | A string that specifies the authenticator assertion response, which contains the signed challenge needed to complete the MFA action. |


### Example Payload to Authenticate Device

```json
{
  "deviceType":"SECURITY_KEY",
  "origin": "https://iam-demo.1dc.com",
  "assertion": "{"id":"jgvYAquTlYLn-7Bx9-fonnsb594GvkH4PKjIELJYx-MAoxfOPfXhgMLy1cXMIZKBxB_mJNNNQF6tOANXhuFelQ","rawId":"jgvYAquTlYLn+7Bx9+fonnsb594GvkH4PKjIELJYx+MAoxfOPfXhgMLy1cXMIZKBxB/mJNNNQF6tOANXhuFelQ==","type":"public-key","response":{"clientDataJSON":"eyJ0eXBlIjoid2ViYXV0aG4uZ2V0IiwiY2hhbGxlbmdlIjoiOHVVQTA2dVB1VFRGNmI2dkhXcTdkZWt6QVo3Y2V2MDMtNnJSQzZoTEFhVSIsIm9yaWdpbiI6Imh0dHBzOi8vaWFtLWRlbW8uMWRjLmNvbSIsImNyb3NzT3JpZ2luIjpmYWxzZSwib3RoZXJfa2V5c19jYW5fYmVfYWRkZWRfaGVyZSI6ImRvIG5vdCBjb21wYXJlIGNsaWVudERhdGFKU09OIGFnYWluc3QgYSB0ZW1wbGF0ZS4gU2VlIGh0dHBzOi8vZ29vLmdsL3lhYlBleCJ9","authenticatorData":"Wvc+/XkaVwxa012pCZWAzWXwWSy8IupI6+2BznkpxM4FAAAACw==","signature":"MEYCIQDp7wBeYYv+02m56wbQaLUstoZWIDxpKI2IvmgeOMUHYQIhAP2W5tDVqKHAQbTsAAZzTdXD/px9ZOtYtIysZyKs4Ws7","userHandle":""}}"
}

<!--
type: tab
-->

### Example of Authenticate Device (200: OK) response

```json
{"status":"SUCCESS","message":"Assertion has been validated successfully "}
```
<!-- type: tab-end -->