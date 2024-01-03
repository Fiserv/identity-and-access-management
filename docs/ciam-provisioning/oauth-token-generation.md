# OAuth Access Token

- Access tokens are credential strings that represent authorization to access a protected resource. Applications obtain access tokens by making OAuth connect requests to an authorization server; CIAM Provisioning API resource servers require clients to authenticate using access tokens. Access tokens are obtained from the token endpoint (when using the client credentials grant type).

- Scopes are used to grant an application different levels of access to data on behalf of the end user. Each API may declare one or more scopes. 

<!--theme: info -->
Here are the list of allowed scopes:
- application.client 
Application client scope for allowed CIAM Provisioning API.

- application.client domain.manage
Application client scope allowed for Delete of App Owned Domain.

---

There are steps required at the application-side that should meet the below criteria:  
- Can make http/REST calls.

- The application is configured via registration process.

- Has the registered application details.


## Getting an access token 

<!--
type: tab
titles: Request, Response
-->

The below table identifies the parameter required for `Application Token Mapping`.

| Variable | Type | Value | Required | Description |
| -------- | -- |------------| ------- | ---- |
| `grant_type` | *string* | client_credentials | &#10004; |  grant type determines the exact sequence of steps that are involved in the OAuth process. |
| `scope` | *string* | application.client domain.manage | &#10004; |  scope defines the access level for the generated token. |


<!--
type: tab
-->

### Example of get application token (200: OK) response

```json

{
    "access_token": "eyJhbGciOiJSUzI1NiIsImtpZCI6InhEUXJsQ2d5bFdOd1M0LVZsZmFhUWZUbjRrbyIsInBpLmF0bSI6InJ6cnUifQ.eyJzY29wZSI6ImFwcGxpY2F0aW9uLmNsaWVudCIsImF1dGhvcml6YXRpb25fZGV0YWlscyI6W10sImNsaWVudF9pZCI6IkFjcnZ6d2RoMCIsImlzcyI6Imh0dHBzOi8vZmRjLWZlZHNzby1kZXYuMWRjLmNvbSIsImF1ZCI6IkFjcnZ6d2RoMCIsImV4cCI6MTY4MjAyODkzNX0.Xn9tFd_3ZmuuBPZPd1rixU38xV_ZfXG7rhq6tzricbmEN-fSS8Ki51vWNS3SndwF-TVKsFZ22xZXF2Apk0-yUGwQNItTcFoRK5y2M-E6-6oWQvePTdiHEqP7utlik9tD7f48IACXfGWH8tP1KsrR3hGAVxdgpDzqJw0ru-FQhjmJe4yewlneHhr_TLlqIF8NjAldn8lXyzALVMmyqMZXd4S0osVblSSHKsRiUn6Kh98VcUnkqaKHu71JVP8-IF0o79Ch2GlOhPJXY42Ffrll5f9VLls4uYf0MLYr4njkOqfOfBmvfYbTXz_ml9chJwQpPbt-X0Zjf50PIxBHfWVnwg",
    "token_type": "Bearer",
    "expires_in": 7199
}

```

<!-- type: tab-end -->