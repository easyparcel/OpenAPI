# Cancel Shipments

This endpoint allows users to cancel one or more shipments. Users can provide a list of shipment numbers along with cancellation remarks.

## HTTP Request (cancel)

`POST https://api.easyparcel.com/open_api/2025-06/shipment/cancel`

## Cancel Request Parameters

### Request Sample

```json
{
    "cancel_list": [
        {
            "shipment_number": "ES-2504-WZ9VY",
            "remark": "test"
        },
        {
            "shipment_number": "ES-2504-K94KU",
            "remark": "test"
        }
    ]
}
```

### Main Structure

| Parameter    | Type    | Required | Description                  |
|--------------|---------|----------|------------------------------|
| cancel_list  | array   | Yes      | List of shipments to cancel  |

### Cancel Item Object

| Parameter       | Type    | Required | Description                   | Remarks                     |
|-----------------|---------|----------|-------------------------------|----------------------------- |
| shipment_number | string  | Yes      | Shipment number to cancel     | Format: ES-YYMM-XXXXX       |
| remark          | string  | Yes      | Reason for cancellation       | -                           |



## Cancel Return Parameters

### Successful Response Example

```json
{
    "status_code": 200,
    "message": "2 requests success, 0 request error.",
    "data": [
        {
            "status": "success",
            "message": "Order Cancelled",
            "shipment_number": "ES-2504-WZ9VY"
        },
        {
            "status": "success",
            "message": "Order Cancelled",
            "shipment_number": "ES-2504-K94KU"
        }
    ]
}
```

### Main Response Structure

| Parameter    | Type    | Description                                               |
|--------------|---------|-----------------------------------------------------------|
| status_code  | int     | Status code of the response                               |
| message      | string  | Summary message (e.g., "2 requests success, 0 request error.") |
| data         | array   | Array of cancellation results                             |

### Cancellation Result Object

| Parameter       | Type    | Description                              |
|-----------------|---------|------------------------------------------|
| status          | string  | Status of the cancellation request ("success" or "error") |
| message         | string  | Detailed message about the cancellation result |
| shipment_number | string  | The shipment number that was processed   |



### Error Response Example

```json
{
    "status_code": 200,
    "message": "0 requests success, 2 request error.",
    "data": [
        {
            "status": "error",
            "message": "Shipment Already Cancelled",
            "shipment_number": "ES-2504-JUB4T"
        },
        {
            "status": "error",
            "message": "Shipment Already Cancelled",
            "shipment_number": "ES-2504-GPC39"
        }
    ]
}
```

## Usage Notes (Cancellation)

1. You can cancel multiple shipments in a single request by including them in the `cancel_list` array.
2. Only shipments that have not yet been processed by the courier can be cancelled.
3. Each shipment in the `cancel_list` will be processed independently - some may succeed while others fail.
4. A successful response (`status_code: 200`) does not guarantee all shipments were cancelled. Always check individual status values in the data array.
5. Cancellation remarks are mandatory and should provide a reason for the cancellation.
6. The API returns a 200 status code even when all cancellations fail, so always check the message and data fields.
