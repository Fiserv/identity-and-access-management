## Get Risk Policy by ID

<!--
type: tab
titles: Request, Response
-->


The below table identifies the parameter required

| Variable | Type | Maximum Length | Required | Description |
| -------- | -- |------------| ------- | ---- |
| `policyId` | *string* | - | &#10004; | A unique ID used to identify the policy. |


<!--
type: tab
-->

### Example of Search Policy By Policy Id (200: Created) response

```json

{
    "message": "Ping Risk Policy retrieved successfully",
    "id": "8af8a047-c97f-4ce1-8f4f-f524f0cd20ce",
    "name": "APM00006238_20230901140371_RISK_POLICY",
    "evaluatedPredictors": [
        {
            "id": "73707b17-8476-0dca-2bfb-4769049b113d"
        },
        {
            "id": "32eb6e4b-1b16-0534-1d05-787b6dd20014"
        },
        {
            "id": "6f6166d1-a133-0131-30f9-b43bf322539e"
        },
        {
            "id": "2cb4bfd5-c55e-02e9-165c-0f25b9b68973"
        },
        {
            "id": "823f486b-3c9f-02b1-05b6-8aa2400985ad"
        },
        {
            "id": "5bf21394-aa62-0ea3-2f2b-1993ed0e55c8"
        },
        {
            "id": "8a46dbcd-844a-0243-3131-086b3b54b02e"
        },
        {
            "id": "f5ad414d-7897-0d90-2e83-4a816abd19eb"
        },
        {
            "id": "2e2576f1-7cb0-09ec-0601-8b56e55ecde7"
        }
    ]
}

```

<!-- type: tab-end -->