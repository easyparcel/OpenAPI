# Couriers List 

This endpoint allows users to retrieve a list of available courier services for a specific country.

## HTTP Request (Courier List)

`GET https://api.easyparcel.com/open_api/2025-12/courier/list`

## Courier List Request

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

## Courier List Response
### Response Sample

```json
{
    "status_code": 200,
    "message": "success",
    "data": [
        {
            "courier_id": "EP-CR0AP",
            "uuid": "01e1cad9-d20a-411f-8c71-a1b3ed722b3f",
            "courier_name": "Aramex",
            "short_name": "Aramex",
            "courier_logo": "https://s3-ap-southeast-1.amazonaws.com/easyparcel-static/Public/source/general/img/couriers/Aramex.jpg",
            "country": "Malaysia"
        },
        {
            "courier_id": "EP-CR0AW",
            "uuid": "db129869-d2cd-474a-b3bf-9995a436ef85",
            "courier_name": "DHL eCommerce",
            "short_name": "DHLeC",
            "courier_logo": "https://s3-ap-southeast-1.amazonaws.com/easyparcel-static/Public/source/general/img/couriers/DHLeC.jpg",
            "country": "Malaysia"
        },
        {
            "courier_id": "EP-CR0AM",
            "uuid": "17bd49e0-f356-41d0-805e-2b6ee8e3d6cc",
            "courier_name": "Poslaju National Courier",
            "short_name": "Pos Laju",
            "courier_logo": "https://s3-ap-southeast-1.amazonaws.com/easyparcel-static/Public/source/general/img/couriers/Pos_Laju.jpg",
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



<h2 id="courierlist-error-response">Error Response</h2>

If an invalid country code is provided, the API will return an error response:

```json
{
    "status_code": 400,
    "message": "Invalid country code",
    "data": []
}
```

## Supported Country Codes

| Country Code | Country Name   |
|--------------|----------------|
| MY           | Malaysia       |
| SG           | Singapore      |

<h2 id="courierlist-common-status-code">Common Status Code</h2>

| Status Code | Description                                     |
|-------------|-------------------------------------------------|
| 200         | Successful request                              |
| 400         | Bad request (invalid country code)              |
| 401         | Unauthorized (invalid authentication)|
| 500         | Server error                                    |

<h2 id="courierlist-usage-notes">Usage Notes (Courier List)</h2>

1. The `courier_id` value returned by this endpoint is used in other API calls, such as when submitting a shipment order.
2. Courier availability may vary by country. Use the appropriate country code to get relevant results.
3. The response includes full company names and shortened display names for each courier.
4. Courier logos can be used in your application to display carrier branding.
5. There may be multiple entries for the same courier company if they offer different types of services.
