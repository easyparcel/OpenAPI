<h1 id="courier-list-2025-06">Couriers List</h1>

This endpoint allows users to retrieve a list of available courier services for a specific country.

<h2 id="http-request-courier-list-2025-06">HTTP Request (Courier List)</h2>

`GET https://api.easyparcel.com/open_api/2025-06/courier/list`

<h2 id="courier-list-requested-parameters-2025-06">Courier List Request</h2>

### Request Sample

```json
{
    "country_code": "MY"
}
```
### Requested Parameters

| Parameter    | Type    | Required | Description                 | Remarks                 |
|--------------|---------|----------|-----------------------------|-------------------------|
| country_code | string  | Yes      | Country code to filter by   | Example: "MY" for Malaysia |




<h2 id="returned-courier-liest-parameters-2025-06">Courier List Response</h2>
### Response Sample

```json
{
    "status_code": 200,
    "message": "success",
    "data": [
        {
            "courier_id": "EP-CR0I",
            "uuid": "c473d2c4-ab06-456a-9886-54a5c3d25c91",
            "courier_name": "SF Global Express",
            "short_name": "SF Express",
            "courier_logo": "https://s3-ap-southeast-1.amazonaws.com/easyparcel/Public/source/general/img/couriers/SF_Express.jpg",
            "country": "Malaysia"
        },
        {
            "courier_id": "EP-CR0G",
            "uuid": "01e1cad9-d20a-411f-8c71-a1b3ed722b3f",
            "courier_name": "Aramex",
            "short_name": "Aramex",
            "courier_logo": "https://s3-ap-southeast-1.amazonaws.com/easyparcel/Public/source/general/img/couriers/Aramex.jpg",
            "country": "Malaysia"
        },
        {
            "courier_id": "EP-CR0AO",
            "uuid": "5e6a0ee2-5d6d-499d-8994-bd71a82730b9",
            "courier_name": "Teleport Commerce Malaysia Sdn Bhd",
            "short_name": "Teleport",
            "courier_logo": "https://s3-ap-southeast-1.amazonaws.com/easyparcel/Public/source/general/img/couriers/Teleport.jpg",
            "country": "Malaysia"
        }
    ]
}
```
### Main Response Structure

| Parameter    | Type    | Description                           |
|--------------|---------|---------------------------------------|
| status_code  | int     | Status code of the response           |
| message      | string  | Response message                      |
| data         | array   | Array of available courier services   |

### Courier Object

| Parameter    | Type    | Description                           |
|--------------|---------|---------------------------------------|
| courier_id   | string  | Unique identifier for the courier     |
| uuid         | string  | Universal unique identifier           |
| courier_name | string  | Full name of the courier company      |
| short_name   | string  | Abbreviated name of the courier       |
| courier_logo | string  | URL to the courier's logo image       |
| country      | string  | Country where the courier operates    |



<h2 id="error-response-2025-06">Error Response</h2>

If an invalid country code is provided, the API will return an error response:

```json
{
    "status_code": 400,
    "message": "Invalid country code",
    "data": []
}
```

<h2 id="supported-country-codes-2025-06">Supported Country Codes</h2>

| Country Code | Country Name   |
|--------------|----------------|
| MY           | Malaysia       |
| SG           | Singapore      |
| TH           | Thailand       |
| ID           | Indonesia      |
| CN           | China          |
| PH           | Philippines    |
| VN           | Vietnam        |
| AU           | Australia      |
| US           | United States  |
| CA           | Canada         |
| GB           | United Kingdom |

<h2 id="common-status-codes-2025-06">Common Status Codes</h2>

| Status Code | Description                                     |
|-------------|-------------------------------------------------|
| 200         | Successful request                              |
| 400         | Bad request (invalid country code)              |
| 401         | Unauthorized (invalid authentication)|
| 500         | Server error                                    |

<h2 id="usage-notes-2025-06">Usage Notes (Courier List)</h2>

1. The `courier_id` value returned by this endpoint is used in other API calls, such as when submitting a shipment order.
2. Courier availability may vary by country. Use the appropriate country code to get relevant results.
3. The response includes full company names and shortened display names for each courier.
4. Courier logos can be used in your application to display carrier branding.
5. There may be multiple entries for the same courier company if they offer different types of services.
