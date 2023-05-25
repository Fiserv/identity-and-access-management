# Create Domain 

- Provisioning API provides a REST API to create a Domain.

There are steps required at the application-side that should meet the below criteria:  

- Can make http/REST calls  

- Has the application Id of an application

- Has the OAuth2 client credentials generated via application.client scope

<!--
type: tab
titles: Request, Response
-->

The below table identifies the parameter required for Domain payload.

| Variable | Type | Maximum Length | Required | Description |
| -------- | -- |------------| ------- | ---- |
| `friendlyName` | *string* | - | &#10004; | friendly name for domain account. |
| `description` | *string* | - | &#10004; | description for domains. |


### Example of Create Domain  payload

```json

{
    "friendlyName": "UAID-12333_Foo Inc",
    "description": "UAID-12333 domain description"
}
```
<!--
type: tab
-->

### Example of Create Domain  (200: Created) response

```json

{
    "domainId": "9d77e19c-ab9a-4820-bdb8-924cd5aad2ee",
    "hasApplicationIds": [
        "Acrvzwdh0"
    ],
    "description": "UAID-12333 domain description",
    "friendlyName": "UAID-12333_Foo Inc",
    "owner": [
        "Acrvzwdh0"
    ]
}

```

<!-- type: tab-end -->