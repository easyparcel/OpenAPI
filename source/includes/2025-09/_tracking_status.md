# Tracking Status Feature

The tracking status feature allows customers to retrieve real-time tracking information for their shipments using AWB (Air Waybill) numbers. This helps users monitor the delivery progress and current status of their parcels.

## Retrieving Tracking Status

Customers can retrieve tracking information for one or multiple shipments using the following endpoint:

## HTTP Request (Tracking Status)

`POST https://api.easyparcel.com/open_api/2025-09/shipment/tracking_status`

This endpoint returns detailed tracking information including the current status, historical events, and location data for each requested shipment.

## Tracking Status Request
### Submitting AWB Numbers to Get Tracking Information

You can submit multiple AWB numbers in a single request to retrieve tracking status for multiple shipments simultaneously.

### Sample Tracking Status Request:

```json
{
  "awb_numbers": ["7227014253232636", "960301021838937", "960301021837659"]
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
    "message": "3 requests success, 0 request error.",
    "data": {
        "results": [
            {
                "status": "success",
                "awb_number": "7227014253232636",
                "shipment_number": "ES-2601-XV7UN",
                "order_number": "EI-2601-U8FZW",
                "latest_shipment_status_code": 7,
                "latest_tracking_status": "Schedule In Arrangement",
                "latest_event_date": "2026-01-23T04:28:52.494Z",
                "status_log": [
                    {
                        "event_date": "2026-01-23 12:29:47",
                        "shipment_status_code": 7,
                        "tracking_status": "Shipment data received - Awaiting Parcel Handover to DHL",
                        "location": "Kuala Lumpur Hub, Kuala Lumpur, MY"
                    },
                    {
                        "event_date": "2026-01-23 12:28:52",
                        "shipment_status_code": 7,
                        "tracking_status": "Data Submitted - Awaiting Parcel Handover to DHL",
                        "location": "BAYAN BARU, PENANG,, PIN, MY"
                    },
                    {
                        "event_date": "2026-01-23T04:28:52.494Z",
                        "shipment_status_code": 7,
                        "tracking_status": "Schedule In Arrangement",
                        "location": null
                    }
                ]
            },
            {
                "status": "success",
                "awb_number": "960301021838937",
                "shipment_number": "ES-2504-X2KV5",
                "order_number": "EI-2504-SKMTH",
                "latest_shipment_status_code": 7,
                "latest_tracking_status": "Schedule In Arrangement",
                "latest_event_date": "2025-04-23 08:13:12",
                "status_log": [
                    {
                        "event_date": "2025-04-23 16:13:00",
                        "shipment_status_code": 7,
                        "tracking_status": "Shipment information sent to City-Link",
                        "location": null
                    },
                    {
                        "event_date": "2025-04-23 08:13:12",
                        "shipment_status_code": 7,
                        "tracking_status": "Schedule In Arrangement",
                        "location": null
                    }
                ]
            },
            {
                "status": "success",
                "awb_number": "960301021837659",
                "shipment_number": "ES-2504-2AE3R",
                "order_number": "EI-2504-WUHYR",
                "latest_shipment_status_code": 7,
                "latest_tracking_status": "Shipment information sent to City-Link",
                "latest_event_date": "2025-04-23 10:46:00",
                "status_log": [
                    {
                        "event_date": "2025-04-23 02:46:36",
                        "shipment_status_code": 7,
                        "tracking_status": "Schedule In Arrangement",
                        "location": null
                    },
                    {
                        "event_date": "2025-04-23 10:46:00",
                        "shipment_status_code": 7,
                        "tracking_status": "Shipment information sent to City-Link",
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
  "awb_numbers": ["7227014253232636"]
}
```

&nbsp;

&nbsp;

### Multiple Shipment Tracking

```json
{
  "awb_numbers": [
  "7227014253232636",
  "960301021838937",
  "960301021837659",
  "1234567890"]
}
```

&nbsp;

&nbsp;

&nbsp;

&nbsp;

### Error Response Example

If one or more AWB numbers are invalid:

```json
{
    "status_code": 200,
    "request_id": "1769761472947.b7a9d539-083a-48d7-8974-0fd6f13baa72",
    "message": "3 requests success, 1 request error.",
    "data": {
        "results": [
            {
                "status": "success",
                "awb_number": "7227014253232636",
                "shipment_number": "ES-2601-XV7UN",
                "order_number": "EI-2601-U8FZW",
                "latest_shipment_status_code": 8,
                "latest_tracking_status": "Cancelled",
                "latest_event_date": "2026-01-30 10:04:18",
                "status_log": [
                    {
                        "event_date": "2026-01-23 12:29:47",
                        "shipment_status_code": 7,
                        "tracking_status": "Shipment data received - Awaiting Parcel Handover to DHL",
                        "location": "Kuala Lumpur Hub, Kuala Lumpur, MY"
                    },
                    {
                        "event_date": "2026-01-23 12:28:52",
                        "shipment_status_code": 7,
                        "tracking_status": "Data Submitted - Awaiting Parcel Handover to DHL",
                        "location": "BAYAN BARU, PENANG,, PIN, MY"
                    },
                    {
                        "event_date": "2026-01-23T04:28:52.494Z",
                        "shipment_status_code": 7,
                        "tracking_status": "Schedule In Arrangement",
                        "location": null
                    },
                    {
                        "event_date": "2026-01-30 10:04:18",
                        "shipment_status_code": 8,
                        "tracking_status": "Cancelled",
                        "location": "Kuala Lumpur Hub, Kuala Lumpur, MY"
                    }
                ]
            },
            {
                "status": "success",
                "awb_number": "960301021838937",
                "shipment_number": "ES-2504-X2KV5",
                "order_number": "EI-2504-SKMTH",
                "latest_shipment_status_code": 7,
                "latest_tracking_status": "Schedule In Arrangement",
                "latest_event_date": "2025-04-23 08:13:12",
                "status_log": [
                    {
                        "event_date": "2025-04-23 16:13:00",
                        "shipment_status_code": 7,
                        "tracking_status": "Shipment information sent to City-Link",
                        "location": null
                    },
                    {
                        "event_date": "2025-04-23 08:13:12",
                        "shipment_status_code": 7,
                        "tracking_status": "Schedule In Arrangement",
                        "location": null
                    }
                ]
            },
            {
                "status": "success",
                "awb_number": "960301021837659",
                "shipment_number": "ES-2504-2AE3R",
                "order_number": "EI-2504-WUHYR",
                "latest_shipment_status_code": 7,
                "latest_tracking_status": "Schedule In Arrangement",
                "latest_event_date": "2025-04-23 02:46:36",
                "status_log": [
                    {
                        "event_date": "2025-04-23 10:46:00",
                        "shipment_status_code": 7,
                        "tracking_status": "Shipment information sent to City-Link",
                        "location": null
                    },
                    {
                        "event_date": "2025-04-23 02:46:36",
                        "shipment_status_code": 7,
                        "tracking_status": "Schedule In Arrangement",
                        "location": null
                    }
                ]
            },
            {
                "awb_number": "1234567890",
                "status": "not_found",
                "message": "AWB number not found"
            }
        ]
    }
}
```



