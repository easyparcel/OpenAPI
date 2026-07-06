<h1 id="hscode-list-2026-06">HS Code List</h1>

This endpoint allows users to retrieve a list of available HS codes.

<h2 id="http-request-hscode-list-2026-06">HTTP Request (HS Code List)</h2>

`GET https://api.easyparcel.com/open_api/2026-06/hscode/list`

<h2 id="returned-hscode-list-parameters-2025-06">HS Code List Response</h2>

### Response Sample

```json
{
    "status_code": 200,
    "message": "Success",
    "data": [
        {
            "hs_code": "4202.12.00",
            "description": "Travel bags and suitcases"
        },
        {
            "hs_code": "8471.30.00",
            "description": "Laptop computers"
        },
        {
            "hs_code": "8517.12.00",
            "description": "Mobile phones"
        }
    ]
}
```

### Main Response Structure

| Parameter    | Type    | Description                           |
|--------------|---------|---------------------------------------|
| status_code  | int     | Status code of the response           |
| message      | string  | Response message                      |
| data         | array   | List of HS codes                      |

### Courier Object

| Parameter    | Type    | Description                           |
|--------------|---------|---------------------------------------|
| hs_code      | string  | HS code value                         |
| description  | string  | Product classification                |

<h2 id="common-status-codes-2026-06">Common Status Codes</h2>

| Status Code | Description                                     |
|-------------|-------------------------------------------------|
| 200         | Successful request                              |
| 400         | Bad request (invalid country code)              |
| 401         | Unauthorized (invalid authentication)           |
| 500         | Server error                                    |

<h2 id="usage-notes-hscode-2026-06">Usage Notes (HS Code List)</h2>

1. This endpoint does not require request parameters.
2. HS codes are used for customs declaration in international shipments.
3. Always use the most updated list for accurate classification.

