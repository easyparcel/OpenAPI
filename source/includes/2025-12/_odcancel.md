# OnDemand Order Cancellation

This guide explains how to cancel an on-demand shipment order.

## Endpoint URL

`POST https://api.easyparcel.com/2025-12/ondemand/cancel`

---

## OnDemand Cancel Request

| Parameter                                                 | Type    | Required | Description                                    |
| --------------------------------------------------------- | ------- | -------- | ---------------------------------------------- |
| booking_id                                                | string  | yes      | booking number/id of the ondemand shipment     |


-
### Request Example

```json
{
    "booking_id": "EOD-150"
}
```

---

## OnDemand Cancel Response

### Sample Response

```json
{
    "status_code": 200,
    "message": "success",
    "data": [
        {
            "message": "Shipment cancelled successfully",
            "booking_id": "EOD-150"
        }
    ]
}
```
### Main Response

| Parameter    | Type   | Description                                |
| ------------ | ------ | ------------------------------------------ |
| status\_code | int    | HTTP status code (e.g., 200)               |
| message      | string | Success or error message                   |
| data         | object | Contains booking details and shipment info |

### Cancellation 

| Parameter      | Type   | Description                          |
| -------------- | ------ | ------------------------------------ |
| message        | string | message for the cancelled status     |
| booking_id     | string | booking id/number of the ondemand status   |


---


<h2 id="odcancel-code-implementation-examples">Code Implementation Examples</h2>

### JavaScript (Fetch API) | PHP (cURL) | Python (Requests)

```javascript
fetch("https://api.easyparcel.com/ondemand/cancel", {
    method: "POST",
    headers: {
        "Content-Type": "application/json",
        "Authorization": "Bearer YOUR_ACCESS_TOKEN"
    },
    body: JSON.stringify({
        booking_id: "EOD-330"
    })
})
.then(res => res.json())
.then(data => console.log(data))
.catch(err => console.error(err));
```

```php
<?php
$ch = curl_init("https://api.easyparcel.com/ondemand/cancel");
$data = [
    "booking_id" => "EOD-330"
];
curl_setopt($ch, CURLOPT_HTTPHEADER, [
    'Content-Type: application/json',
    'Authorization: Bearer YOUR_ACCESS_TOKEN'
]);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode($data));
$response = curl_exec($ch);
curl_close($ch);
echo $response;
?>
```

```python
import requests

url = "https://api.easyparcel.com/ondemand/cancel"
headers = {
    "Content-Type": "application/json",
    "Authorization": "Bearer YOUR_ACCESS_TOKEN"
}
data = {
    "booking_id": "EOD-330"
}
response = requests.post(url, json=data, headers=headers)
print(response.json())
```

## Best Practices for Ondemand Cancel Order

* **Always include a valid `booking_id`** when attempting to cancel an order.
* **Ensure the order is eligible for cancellation** (i.e., not already picked up or completed).
* **Handle the response gracefully**, including possible failure messages.
* **Use test credentials** in sandbox mode for testing integration before going live.
* **Rate limit your API calls** to avoid service throttling or rejection.
* **Log your cancellation attempts** for traceability and support reference.
* **Secure your access token** and never expose it in public repositories or front-end code.
