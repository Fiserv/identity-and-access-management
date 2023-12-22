# OAuth Access Token

- Access tokens are credential strings that represent authorization to access a protected resource. Applications obtain access tokens by making OAuth connect requests to an authorization server; CIAM Provisioning API resource servers require clients to authenticate using access tokens. Access tokens are obtained from the token endpoint (when using the client credentials grant type).

- You need to provide client_id, client_secret and grant_type(fixed, "client_credential") as request payload.

- To get client_id and client_secret, onboard your application through CIAM self service portal, you will receive these credential as mail.

There are steps required at the application-side that should meet the below criteria:  
- Can make http/REST calls.

- The application is configured via onboarding process.

- Has the registered application details.

The below table identifies the parameter required for `Application Token Mapping`.

| Variable | Type | Value | Required | Description |
| -------- | -- |------------| ------- | ---- |
| `grant_type` | *string* | client_credentials | &#10004; |  grant type determines the exact sequence of steps that are involved in the OAuth process. |
| `client_id` | *string* | which is received on mail | &#10004; | The cient id which is received while onboarding the application |
| `client_secret` | *string* | which is received on mail | &#10004; | The cient secret which is received while onboarding the application |


<!--
type: tab
titles: Request, Response
-->

Endpoint **:**

**POST** [{{base_url}}/ciam-mfa/v2/get/token](../api/?type=post&path=/ciam-mfa/v2/get/token&version=2.0.0)

**Payload** **:**

```json
{
    "grant_type":"client_credential",
    "client_id":"Sfq5hn4nf",
    "client_secret":"S^7j|)v,Zd"
}
```

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