<h1 id="shipment-listing-2025-06">Shipment Listing</h1>

This endpoint allows users to retrieve a list of shipments with optional filtering parameters. Results are sorted by the latest shipments first.

<h2 id="http-request-listing-2025-06">HTTP Request (Listing)</h2>

`POST https://api.easyparcel.com/open_api/2025-06/shipment/list`


<h2 id="listing-request-2025-06">Listing Request</h2>

<h2 id="pagination-2025-06">Pagination</h2>

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
  "before_shipment_number": "ES-2601-3MMYQ",
  "shipment_status_code": "7",
  "date_from": "2025-04-01",
  "date_to": "2025-04-20"
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



<h2 id="shipment-listing-returned-parameters-2025-06">Returned Parameters</h2>

### Response Sample

```json
{
    "status_code": 200,
    "message": "success",
    "data": [
        {
            "shipment_number": "ES-2504-XYQUA",
            "awb_number": null,
            "awb_url": null,
            "tracking_url": null,
            "shipment_status_code": 7,
            "shipment_status": "Schedule In Arrangement",
            "coll_date": "2025-04-22 16:00:00",
            "courier": {
                "service_type": "Mystery Saver",
                "courier_id": "EP-CR0AT",
                "service_id": "EP-CS0AT",
                "courier_name": "TracX Logis Pte. Ltd",
                "courier_short_name": "TRACX LOGIS",
                "courier_logo": "https://s3-ap-southeast-1.amazonaws.com/easyparcel-static/Public/source/general/img/couriers/"
            },
            "sender_details": {
                "name": "testSG",
                "email": "ep@easyparcel.com",
                "contact": "SG88888888",
                "alternative_contact": 0,
                "address1": "test sg",
                "subdivision_code": "SG-04",
                "postal_code": "409015",
                "country": "SG"
            },
            "receiver_details": {
                "name": "testSG",
                "email": "ep@easyparcel.com",
                "contact": "SG88888888",
                "alternative_contact": 0,
                "subdivision_code": "SG-04",
                "postal_code": "409015",
                "country": "SG"
            },
            "pricing": {
                "currency_code": "MYR",
                "price": 16.99
            }
        },
        {
            "shipment_number": "ES-2504-B4H35",
            "awb_number": null,
            "awb_url": null,
            "tracking_url": null,
            "shipment_status_code": 7,
            "shipment_status": "Schedule In Arrangement",
            "coll_date": "2025-04-22 16:00:00",
            "courier": {
                "service_type": "Mystery Saver",
                "courier_id": "EP-CR0AT",
                "service_id": "EP-CS0AT",
                "courier_name": "TracX Logis Pte. Ltd",
                "courier_short_name": "TRACX LOGIS",
                "courier_logo": "https://s3-ap-southeast-1.amazonaws.com/easyparcel-static/Public/source/general/img/couriers/"
            },
            "sender_details": {
                "name": "testSG",
                "email": "ep@easyparcel.com",
                "contact": "SG88888888",
                "alternative_contact": 0,
                "address1": "test sg",
                "subdivision_code": "SG-04",
                "postal_code": "409015",
                "country": "SG"
            },
            "receiver_details": {
                "name": "testSG",
                "email": "ep@easyparcel.com",
                "contact": "SG88888888",
                "alternative_contact": 0,
                "subdivision_code": "SG-04",
                "postal_code": "409015",
                "country": "SG"
            },
            "pricing": {
                "currency_code": "MYR",
                "price": 16.99
            }
        },
        {
            "shipment_number": "ES-2504-4XMAY",
            "awb_number": null,
            "awb_url": null,
            "tracking_url": null,
            "shipment_status_code": 7,
            "shipment_status": "Schedule In Arrangement",
            "coll_date": "2025-04-22 16:00:00",
            "courier": {
                "service_type": "Mystery Saver",
                "courier_id": "EP-CR0AT",
                "service_id": "EP-CS0AT",
                "courier_name": "TracX Logis Pte. Ltd",
                "courier_short_name": "TRACX LOGIS",
                "courier_logo": "https://s3-ap-southeast-1.amazonaws.com/easyparcel-static/Public/source/general/img/couriers/"
            },
            "sender_details": {
                "name": "testSG",
                "email": "ep@easyparcel.com",
                "contact": "SG88888888",
                "alternative_contact": 0,
                "address1": "test sg",
                "subdivision_code": "SG-04",
                "postal_code": "409015",
                "country": "SG"
            },
            "receiver_details": {
                "name": "testSG",
                "email": "ep@easyparcel.com",
                "contact": "SG88888888",
                "alternative_contact": 0,
                "subdivision_code": "SG-04",
                "postal_code": "409015",
                "country": "SG"
            },
            "pricing": {
                "currency_code": "MYR",
                "price": 16.99
            }
        }
    ],
    "pagination": {
        "next_page_token": "eyJsYXN0X2lkIjoyNTg2OSwiZmlsdGVycyI6eyJ0cmFja2luZ19zdGF0dXMiOiI3IiwiZGF0ZV9mcm9tIjoiMjAyNS0wNC0wMSAwMDowMDowMCIsImRhdGVfdG8iOiIyMDI1LTA0LTIwIDIzOjU5OjU5In19",
        "next_shipment_number": "ES-2504-4XMAY",
        "has_more": true,
        "limit": 3,
        "filter_applied": {
            "tracking_status": "7",
            "date_from": "2025-04-01 00:00:00",
            "date_to": "2025-04-20 23:59:59",
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



<h2 id="common-status-codes-1">Common Status Code</h2>

| Status Code | Description                                          |
|-------------|------------------------------------------------------|
| 200         | Successful request                                   |
| 400         | Bad request (missing or invalid parameters)          |
| 401         | Unauthorized (invalid authentication)                |
| 404         | Not found (no shipments matching the criteria)       |
| 500         | Server error                                         |

<h2 id="shipment-listing-usage-notes-2025-06">Usage Notes (Listing)</h2>

1. For pagination, use the `before_shipment_number` parameter with the last shipment number from the previous request.
2. Date filters (`date_from` and `date_to`) filter by shipment collection date.
3. Results are always sorted by newest first.
4. When no filters are applied, the API returns the most recent shipments up to the specified limit.

---
