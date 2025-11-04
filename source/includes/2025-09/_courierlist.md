# Couriers List 

This endpoint allows users to retrieve a list of available courier services for a specific country.

## HTTP Request (Courier list)

`GET https://api.easyparcel.com/open_api/2025-06/courier/list`

## Courier List Requested Parameters

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




## Returned Courier list Parameters
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



## Error Response

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
| TH           | Thailand       |
| ID           | Indonesia      |
| CN           | China          |
| PH           | Philippines    |
| VN           | Vietnam        |
| AU           | Australia      |
| US           | United States  |
| CA           | Canada         |
| GB           | United Kingdom |

## Common Status Codes

| Status Code | Description                                     |
|-------------|-------------------------------------------------|
| 200         | Successful request                              |
| 400         | Bad request (invalid country code)              |
| 401         | Unauthorized (invalid authentication)|
| 500         | Server error                                    |

## Usage Notes

1. The `courier_id` value returned by this endpoint is used in other API calls, such as when submitting a shipment order.
2. Courier availability may vary by country. Use the appropriate country code to get relevant results.
3. The response includes full company names and shortened display names for each courier.
4. Courier logos can be used in your application to display carrier branding.
5. There may be multiple entries for the same courier company if they offer different types of services.
