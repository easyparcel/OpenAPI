# Tracking Status Feature

The tracking status feature allows customers to retrieve real-time tracking information for their shipments using AWB (Air Waybill) numbers. This helps users monitor the delivery progress and current status of their parcels.

## Retrieving Tracking Status

Customers can retrieve tracking information for one or multiple shipments using the following endpoint:

### HTTP Request (Tracking Status)

`POST https://api.easyparcel.com/open_api/2025-09/shipment/tracking_status`

This endpoint returns detailed tracking information including the current status, historical events, and location data for each requested shipment.

## Tracking Status Request

### Submitting AWB Numbers to Get Tracking Information

You can submit multiple AWB numbers in a single request to retrieve tracking status for multiple shipments simultaneously.

### Sample Tracking Status Request:

```json
{
  "awb_numbers": ["631888951038", "631884685186", "631883534779"]
}
```

### Request Parameters

| Parameter    | Type  | Required | Description                                    |
|--------------|-------|----------|------------------------------------------------|
| awb_numbers  | array | Yes      | List of AWB numbers to track (max 100 per request) |

## Tracking Status Response

### Tracking Status API - Response Parameters

### Sample Response for Tracking Status

```json
{
    "status_code": 200,
    "request_id": "1762483800565.37b3a079-d925-4c17-8c16-5e39aa7694ad",
    "message": "3 requests success, 0 request error.",
    "data": {
        "results": [
            {
                "status": "success",
                "awb_number": "631888951038",
                "shipment_number": "ES-2511-97KPC",
                "order_number": "EI-2511-3D2BJ",
                "latest_shipment_status_code": 7,
                "latest_tracking_status": "Schedule In Arrangement",
                "latest_event_date": "2025-11-04 12:20:10",
                "status_log": [
                    {
                        "event_date": "2025-11-04 12:20:10",
                        "shipment_status_code": 7,
                        "tracking_status": "Schedule In Arrangement",
                        "location": null
                    }
                ]
            },
            {
                "status": "success",
                "awb_number": "631884685186",
                "shipment_number": "ES-2511-EFRNN",
                "order_number": "EI-2511-UJUVQ",
                "latest_shipment_status_code": 7,
                "latest_tracking_status": "Schedule In Arrangement",
                "latest_event_date": "2025-11-04 12:14:40",
                "status_log": [
                    {
                        "event_date": "2025-11-04 12:14:40",
                        "shipment_status_code": 7,
                        "tracking_status": "Schedule In Arrangement",
                        "location": null
                    }
                ]
            },
            {
                "status": "success",
                "awb_number": "631883534779",
                "shipment_number": "ES-2510-S2XXR",
                "order_number": "EI-2510-YK93B",
                "latest_shipment_status_code": 7,
                "latest_tracking_status": "Schedule In Arrangement",
                "latest_event_date": "2025-10-31 09:31:27",
                "status_log": [
                    {
                        "event_date": "2025-10-31 09:31:27",
                        "shipment_status_code": 7,
                        "tracking_status": "Schedule In Arrangement",
                        "location": null
                    }
                ]
            }
        ]
    }
}
```

### Main Response

| Parameter    | Type   | Description                                             |
|--------------|--------|---------------------------------------------------------|
| status_code  | int    | HTTP status code indicating success or failure          |
| request_id   | string | Unique identifier for the API request                   |
| message      | string | Summary of the response (e.g., number of successful/failed requests) |
| data         | object | Container for tracking results                          |

### `data` Object

| Parameter | Type  | Description                                    |
|-----------|-------|------------------------------------------------|
| results   | array | List of tracking result objects for each AWB   |

### `result` Object (Inside `results` array)

| Parameter                    | Type   | Description                                                      |
|------------------------------|--------|------------------------------------------------------------------|
| status                       | string | Status of the tracking request ("success" or "not_found")        |
| awb_number                   | string | Air Waybill number for the shipment                              |
| shipment_number              | string | EasyParcel shipment reference number (only for successful requests) |
| order_number                 | string | EasyParcel order reference number (only for successful requests) |
| latest_shipment_status_code  | int    | Numeric code representing the current shipment status (only for successful requests) |
| latest_tracking_status       | string | Human-readable description of the current status (only for successful requests) |
| latest_event_date            | string | Date and time of the most recent tracking event (YYYY-MM-DD HH:MM:SS) (only for successful requests) |
| status_log                   | array  | Chronological list of all tracking events for this shipment (only for successful requests) |
| message                      | string | Error message explaining why the request failed (only for failed requests) |

### `status_log` Object (Inside `status_log` array)

| Parameter              | Type   | Description                                                 |
|------------------------|--------|-------------------------------------------------------------|
| event_date             | string | Date and time when this event occurred (YYYY-MM-DD HH:MM:SS) |
| shipment_status_code   | int    | Numeric code representing the shipment status at this event |
| tracking_status        | string | Human-readable description of the status at this event      |
| location               | string | Location where the event occurred (null if not available)   |

---

## Shipment Status Codes

Below are common shipment status codes you may encounter:

| Status Code | Description                    |
|-------------|--------------------------------|
| 1           | Order Created                  |
| 2           | Payment Confirmed              |
| 3           | Ready for Collection           |
| 4           | Item Collected                 |
| 5           | In Transit to Hub              |
| 6           | Processing at Hub              |
| 7           | Schedule In Arrangement        |
| 8           | Out for Delivery               |
| 9           | Delivered                      |
| 10          | Delivery Failed                |
| 11          | Return to Sender               |

*Note: Status codes may vary by courier and region. Refer to the API response for the most accurate status description.*


## Usage Notes (Tracking)

- **Batch Tracking**: You can track up to 100 AWB numbers in a single API request for efficiency.
- **Real-time Updates**: Tracking information is updated in near real-time as events are recorded by the courier.
- **Status Log**: The `status_log` array provides a complete history of all tracking events in chronological order.
- **Error Handling**: If an AWB number is invalid or not found, the corresponding result object will have `status: "not_found"` with a descriptive message field.
- **Date Format**: All dates and times are returned in `YYYY-MM-DD HH:MM:SS` format in UTC timezone.


## Example Use Cases

### Single Shipment Tracking

```json
{
  "awb_numbers": ["631888951038"]
}
```

### Multiple Shipment Tracking

```json
{
  "awb_numbers": [
    "631888951038",
    "631884685186",
    "631883534779",
    "631882123456"
  ]
}
```

### Error Response Example

If one or more AWB numbers are invalid:

```json
{
    "status_code": 200,
    "request_id": "1762484144652.acff66b7-9994-44cb-8821-e09666765c3d",
    "message": "2 requests success, 1 request error.",
    "data": {
        "results": [
            {
                "status": "success",
                "awb_number": "631888951038",
                "shipment_number": "ES-2511-97KPC",
                "order_number": "EI-2511-3D2BJ",
                "latest_shipment_status_code": 7,
                "latest_tracking_status": "Schedule In Arrangement",
                "latest_event_date": "2025-11-04 12:20:10",
                "status_log": [
                    {
                        "event_date": "2025-11-04 12:20:10",
                        "shipment_status_code": 7,
                        "tracking_status": "Schedule In Arrangement",
                        "location": null
                    }
                ]
            },
            {
                "status": "success",
                "awb_number": "631884685186",
                "shipment_number": "ES-2511-EFRNN",
                "order_number": "EI-2511-UJUVQ",
                "latest_shipment_status_code": 7,
                "latest_tracking_status": "Schedule In Arrangement",
                "latest_event_date": "2025-11-04 12:14:40",
                "status_log": [
                    {
                        "event_date": "2025-11-04 12:14:40",
                        "shipment_status_code": 7,
                        "tracking_status": "Schedule In Arrangement",
                        "location": null
                    }
                ]
            },
            {
                "awb_number": "683534779",
                "status": "not_found",
                "message": "AWB number not found"
            }
        ]
    }
}
```



