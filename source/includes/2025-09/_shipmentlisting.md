# Shipment Listing

This endpoint allows users to retrieve a list of shipments with optional filtering parameters. Results are sorted by the latest shipments first.

## HTTP Request (Listing)

`POST https://api.easyparcel.com/open_api/2025-09/shipment/list`

## Pagination

This API uses cursor-based pagination with the `before_shipment_number` parameter. To retrieve the next page of results:

1. Make your initial request with desired filters and `limit`
2. Note the `shipment_number` of the last shipment in the response
3. Use that shipment number as `before_shipment_number` in your next request to get older shipments

**Example:**
```json
// First request
{ "limit": 10 }

// Next page request (using last shipment_number from previous response)
{ "limit": 10, "before_shipment_number": "ES-2504-3WYYP" }
```

Since results are sorted newest first, each subsequent request returns the next set of older shipments.

### Request Sample

```json
{
  "limit": 3,
  "before_shipment_number": "ES-2505-8WZ3Z",
  "shipment_status_code": "7",
  "date_from": "2025-04-01",
  "date_to": "2025-04-23"
}
```

> Note: You can submit a request without any filters, but the maximum limit is 250 shipments per API call. Results are sorted with the latest shipments first.

### Main Structure

| Parameter               | Type        | Required | Description                                | Remarks                                     |
|-------------------------|-------------|----------|--------------------------------------------|---------------------------------------------|
| limit                   | int         | No       | Maximum number of results to return        | Default: 10, Maximum: 250                   |
| before_shipment_number  | string      | No       | Get shipments before this shipment number  | For pagination purposes                     |
| shipment_status_code    | string      | No       | Filter by shipment status code             | Example: "7" for "Schedule In Arrangement"  |
| date_from               | date        | No       | Start date for filtering shipments         | Format: YYYY-MM-DD                          |
| date_to                 | date        | No       | End date for filtering shipments           | Format: YYYY-MM-DD                          |

## Returned Parameters
### Response Sample

```json
{
    "status_code": 200,
    "request_id": "1768812992614.b1b57f32-6b67-4a6b-bc78-d9e89277f45d",
    "message": "success",
    "data": [
        {
            "shipment_number": "ES-2504-X2KV5",
            "awb_number": "960301021838937",
            "awb_url": "https://s3-ap-southeast-1.amazonaws.com/easyparcel-static/Public/courier/consignment_note/49854776-1dda-4c4b-9bad-f66157e8f6b4.pdf",
            "tracking_url": "https://app.easyparcel.com/tools/easytrack/details?courier=City-Link Express&awb=960301021838937",
            "shipment_status_code": 7,
            "shipment_status": "Schedule In Arrangement",
            "coll_date": "2025-04-30 00:00:00",
            "courier": {
                "service_type": "City-Link Express (Drop-Off)",
                "courier_id": "EP-CR0D9",
                "service_id": "EP-CS0D9",
                "courier_name": "City-Link Express (M) Sdn. Bhd.",
                "courier_short_name": "City-Link Express",
                "courier_logo": "https://s3-ap-southeast-1.amazonaws.com/easyparcel-static/Public/source/general/img/couriers/"
            },
            "sender_details": {
                "name": "Afiq",
                "email": "afiq@easyparcel.com",
                "contact": "MY124651303",
                "alternative_contact": 0,
                "address1": "No 4",
                "subdivision_code": "MY-02",
                "postal_code": "06000",
                "country": "MY"
            },
            "receiver_details": {
                "name": "Afiq Receiver",
                "email": "afiq@easyparcel.com",
                "contact": "MY124651303",
                "alternative_contact": 0,
                "subdivision_code": "MY-07",
                "postal_code": "11900",
                "country": "MY"
            },
            "pricing": {
                "currency_code": "MYR",
                "price": 5.65
            }
        },
        {
            "shipment_number": "ES-2504-2AE3R",
            "awb_number": "960301021837659",
            "awb_url": "https://s3-ap-southeast-1.amazonaws.com/easyparcel-static/Public/courier/consignment_note/17306a0f-f6e9-40ea-9957-c1d1e53d7692.pdf",
            "tracking_url": "https://app.easyparcel.com/tools/easytrack/details?courier=City-Link Express&awb=960301021837659",
            "shipment_status_code": 7,
            "shipment_status": "Schedule In Arrangement",
            "coll_date": "2025-04-28 00:00:00",
            "courier": {
                "service_type": "City-Link Express (Drop-Off)",
                "courier_id": "EP-CR0D9",
                "service_id": "EP-CS0D9",
                "courier_name": "City-Link Express (M) Sdn. Bhd.",
                "courier_short_name": "City-Link Express",
                "courier_logo": "https://s3-ap-southeast-1.amazonaws.com/easyparcel-static/Public/source/general/img/couriers/"
            },
            "sender_details": {
                "name": "test afiq kedah",
                "email": "afiq@easyparcel.com",
                "contact": "MY124651303",
                "alternative_contact": 0,
                "address1": "taman suria 5",
                "subdivision_code": "MY-02",
                "postal_code": "06000",
                "country": "MY"
            },
            "receiver_details": {
                "name": "Test afiq penang",
                "email": "afiq@easyparcel.com",
                "contact": "MY124651303",
                "alternative_contact": 0,
                "subdivision_code": "MY-07",
                "postal_code": "11900",
                "country": "MY"
            },
            "pricing": {
                "currency_code": "MYR",
                "price": 5.65
            }
        },
        {
            "shipment_number": "ES-2504-QBURU",
            "awb_number": "960301021837651",
            "awb_url": "https://s3-ap-southeast-1.amazonaws.com/easyparcel-static/Public/courier/consignment_note/ca605e9f-5a24-47cb-a6cb-f1e9590de3d5.pdf",
            "tracking_url": "https://app.easyparcel.com/tools/easytrack/details?courier=City-Link Express&awb=960301021837651",
            "shipment_status_code": 7,
            "shipment_status": "Schedule In Arrangement",
            "coll_date": "2025-04-29 00:00:00",
            "courier": {
                "service_type": "City-Link Express (Drop-Off)",
                "courier_id": "EP-CR0D9",
                "service_id": "EP-CS0D9",
                "courier_name": "City-Link Express (M) Sdn. Bhd.",
                "courier_short_name": "City-Link Express",
                "courier_logo": "https://s3-ap-southeast-1.amazonaws.com/easyparcel-static/Public/source/general/img/couriers/"
            },
            "sender_details": {
                "name": "test afiq kedah",
                "email": "afiq@easyparcel.com",
                "contact": "MY124651303",
                "alternative_contact": 0,
                "address1": "taman suria 5",
                "subdivision_code": "MY-02",
                "postal_code": "06000",
                "country": "MY"
            },
            "receiver_details": {
                "name": "Test afiq penang",
                "email": "afiq@easyparcel.com",
                "contact": "MY124651303",
                "alternative_contact": 0,
                "subdivision_code": "MY-07",
                "postal_code": "11900",
                "country": "MY"
            },
            "pricing": {
                "currency_code": "MYR",
                "price": 5.65
            }
        }
    ],
    "pagination": {
        "next_page_token": "eyJsYXN0X2lkIjoyNzE0MywiZmlsdGVycyI6eyJ0cmFja2luZ19zdGF0dXMiOiI3IiwiZGF0ZV9mcm9tIjoiMjAyNS0wNC0wMSAwMDowMDowMCIsImRhdGVfdG8iOiIyMDI1LTA0LTIzIDIzOjU5OjU5In19",
        "next_shipment_number": "ES-2504-QBURU",
        "has_more": true,
        "limit": 3,
        "filter_applied": {
            "tracking_status": "7",
            "date_from": "2025-04-01 00:00:00",
            "date_to": "2025-04-23 23:59:59",
            "tracking_status_code": "7"
        }
    }
}
```

### Main Response Structure

| Parameter           | Type      | Description                                |
|---------------------|-----------|--------------------------------------------|
| status_code         | int       | Status code of the response                |
| message             | string    | Response message                           |
| data                | array     | Array of shipment objects                  |

### Shipment Object

| Parameter           | Type      | Description                                |
|---------------------|-----------|--------------------------------------------|
| shipment_number     | string    | Unique shipment identifier                 |
| awb                 | string    | Airway bill number (null if not assigned)  |
| shipment_status_code| int       | Status code of the shipment                |
| shipment_status     | string    | Human-readable shipment status             |
| coll_date           | string    | Collection date and time                   |
| courier             | object    | Courier information                        |
| sender_details      | object    | Sender information                         |
| receiver_details    | object    | Receiver information                       |
| pricing             | object    | Pricing information                        |

### Courier Object

| Parameter           | Type      | Description                                |
|---------------------|-----------|--------------------------------------------|
| service_type        | string    | Type of courier service                    |
| courier_id          | string    | Unique identifier for the courier          |
| service_id          | string    | Unique identifier for the service          |
| courier_name        | string    | Full name of the courier company           |
| courier_short_name  | string    | Short name of the courier company          |
| courier_logo        | string    | URL to the courier logo image              |

### Sender Details Object

| Parameter           | Type      | Description                                |
|---------------------|-----------|--------------------------------------------|
| name                | string    | Name of the sender                         |
| email               | string    | Email address of the sender                |
| contact             | string    | Contact number with country code           |
| alternative_contact | string/int| Alternative contact number (0 if none)     |
| address1            | string    | First line of the sender's address         |
| subdivision_code    | string    | State/province code (null if not provided) |
| postal_code         | string    | Postal/ZIP code                            |
| country             | string    | Country code                               |

### Receiver Details Object

| Parameter           | Type      | Description                                |
|---------------------|-----------|--------------------------------------------|
| name                | string    | Name of the receiver                       |
| email               | string    | Email address of the receiver              |
| contact             | string    | Contact number with country code           |
| alternative_contact | string/int| Alternative contact number (0 if none)     |
| subdivision_code    | string    | State/province code (null if not provided) |
| postal_code         | string    | Postal/ZIP code                            |
| country             | string    | Country code                               |

### Pricing Object

| Parameter           | Type      | Description                                |
|---------------------|-----------|--------------------------------------------|
| currency_code       | string    | Currency code for the price                |
| price               | double    | Price of the shipment                      |

## Common Status Codes

| Status Code | Description                                          |
|-------------|------------------------------------------------------|
| 200         | Successful request                                   |
| 400         | Bad request (missing or invalid parameters)          |
| 401         | Unauthorized (invalid authentication)                |
| 404         | Not found (no shipments matching the criteria)       |
| 500         | Server error                                         |

## Usage Notes (Listing)

1. For pagination, use the `before_shipment_number` parameter with the last shipment number from the previous request.
2. Date filters (`date_from` and `date_to`) filter by shipment collection date.
3. Results are always sorted by newest first.
4. When no filters are applied, the API returns the most recent shipments up to the specified limit.

---
