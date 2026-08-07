<h1 id="od-order-details-2026-06">OnDemand Order Details</h1>

<h2 id="od-order-details-overview-2026-06">OnDemand Order Details Overview</h2>

This feature allows users to retrieve the full detail of a single on-demand order booked through the EasyParcel platform. Given a `booking_id` (obtainable from the [OnDemand Shipment Listing](#od-shipment-listing-2026-06) endpoint), the response returns the order status, pickup window, assigned driver, courier and transport information, every waypoint with its parcel/item breakdown and proof of delivery, and the full pricing breakdown.

The order is always resolved against the wallet of the account behind the access token — an order that does not belong to the authenticated account is rejected.

<h2 id="http-request-od-order-details-2026-06">HTTP Request (OnDemand Order Details)</h2>

`POST https://api.easyparcel.com/open_api/2026-06/ondemand/details`

<h2 id="od-order-details-request-parameters-2026-06">OnDemand Order Details Request Parameters</h2>

### Request Sample

```json
{
  "booking_id": "EOD-98765"
}
```

### Main Structure

| Parameter    | Type   | Required | Description                                  | Remarks                                                                              |
| ------------ | ------ | -------- | -------------------------------------------- | ------------------------------------------------------------------------------------ |
| booking\_id  | string | Yes      | EasyParcel on-demand booking ID              |                                                                                      |

<h2 id="response-parameters-od-order-details-2026-06">OnDemand Order Details Response Parameters</h2>

### Sample Response

```json
{
    "status_code": 200,
    "request_id": "1770000000000.a1b2c3d4-e5f6-7890-abcd-ef1234567890",
    "message": "success",
    "data": [
        {
            "booking_id": "EOD-98765",
            "order_number": "355123433231311221",
            "status": 3,
            "status_text": "In Transit",
            "pickup_time_from": "2026-06-18 11:00:00",
            "pickup_time_to": "2026-06-18 11:30:00",
            "driver": {
                "name": "John Doe",
                "phone": "60123456789",
                "photo": "https://randomphoto.com",
                "rating": "4.9",
                "vehicle": {
                    "license_plate": "ABC 1234",
                    "model": "Honda EX5",
                    "type": "MOTORCYCLE"
                },
                "coordinates": {
                    "latitude": 5.3341,
                    "longitude": 100.2841
                }
            },
            "courier": {
                "courier_name": "Lalamove",
                "service_id": "EP-CS0F",
                "courier_id": "EP-CR03",
                "courier_logo": "https://s3-ap-southeast-1.amazonaws.com/easyparcel-static/Public/source/general/img/couriers/lalamove.svg"
            },
            "transport": {
                "tracking_url": "https://test3.com",
                "transportation_type": "Bike",
                "service_types": {
                    "weight_limit": "10kg",
                    "dimension": "30cmx30cmx30cm",
                    "parcel_type_support": "Parcel"
                }
            },
            "waypoint": [
                {
                    "delivery_id": "3418817446741394383",
                    "name": "ABCXYZ Trading Sdn Bhd",
                    "email": "test@gmail.com",
                    "address": "Kawasan Mendaki Bukit Jambul, Lintang Bukit Jambul 1, Bukit Jambul Indah, Bayan Lepas, 11900, Pulau Pinang, Malaysia",
                    "unit_number": "",
                    "phone_number_country_code": "60",
                    "phone_number": "123456789",
                    "type": 1,
                    "note": "Collect at the front counter",
                    "pod": null,
                    "coordinate": {
                        "latitude": 5.342720241204454,
                        "longitude": 100.28204988381822
                    },
                    "packages": []
                },
                {
                    "delivery_id": "3418744446755394384",
                    "name": "John Tan",
                    "email": "john@example.com",
                    "address": "Suntech @ Penang Cybercity, 1, Lintang Mayang Pasir 3, Bandar Bayan Baru, Bayan Lepas, 11950, Pulau Pinang, Malaysia",
                    "unit_number": "",
                    "phone_number_country_code": "60",
                    "phone_number": "11231241323",
                    "type": 2,
                    "note": "Leave at guard house if not around",
                    "pod": null,
                    "coordinate": {
                        "latitude": 5.325513957,
                        "longitude": 100.2862732
                    },
                    "packages": [
                        {
                            "description": "Documents",
                            "quantity": 1,
                            "dimensions": {
                                "weight": 1,
                                "width": 20,
                                "height": 5,
                                "length": 30
                            }
                        }
                    ]
                }
            ],
            "pricing": {
                "currency_code": "MYR",
                "total_price": "5.88",
                "shipment_price": "5.88",
                "tax_amount": "0.00"
            }
        }
    ]
}
```

### Main Structure

| Parameter    | Type   | Description                                                              |
| ------------ | ------ | ------------------------------------------------------------------------ |
| status\_code | int    | HTTP status code                                                         |
| request\_id  | string | Unique request identifier                                                |
| message      | string | Status message                                                           |
| data         | array  | Array containing the matched order. Contains a single entry on success   |

> **`data` is an array.** Even though `booking_id` resolves to at most one order, the response wraps it in an array for consistency with the listing endpoint. Read `data[0]`.

### Order Object Structure

| Section   | Parameter              | Type             | Description                                                                        |
| --------- | ---------------------- | ---------------- | ---------------------------------------------------------------------------------- |
| —         | booking\_id            | string           | EasyParcel booking ID, prefixed `EOD-`                                             |
| —         | order\_number          | string           | On-demand order number. Empty string when not yet assigned                         |
| —         | status                 | int              | Status code — see [Status Codes](#status-codes-od-order-details-2026-06)           |
| —         | status\_text           | string           | Human readable status                                                              |
| —         | pickup\_time\_from     | datetime         | Start of the scheduled pickup window                                               |
| —         | pickup\_time\_to       | datetime         | End of the scheduled pickup window                                                 |
| —         | driver                 | object \| null   | Assigned driver. `null` until a driver is assigned — see [Driver Object](#driver-object-od-order-details-2026-06) |
| courier   | courier\_name          | string           | Courier short name (e.g. `Lalamove`, `PandaGo`)                                    |
|           | service\_id            | string           | EasyParcel service ID (e.g. `EP-CS0F`)                                             |
|           | courier\_id            | string           | EasyParcel courier ID (e.g. `EP-CR03`)                                             |
|           | courier\_logo          | string           | Courier logo URL                                                                   |
| transport | tracking\_url          | string           | Public tracking URL for the shipment                                               |
|           | transportation\_type   | string           | Transport type (e.g. `Bike`, `Car`, `Van`)                                         |
|           | service\_types         | object \| string | Service metadata for the selected transport (weight/dimension limits, parcel support). Empty string when not configured |
| waypoint  | waypoint\[]            | array            | Pickup and dropoff points — see [Waypoint Object](#waypoint-object-od-order-details-2026-06) |
| pricing   | currency\_code         | string           | Currency of the charged amounts (e.g. `MYR`)                                       |
|           | total\_price           | string           | Total credit deducted for this order                                               |
|           | shipment\_price        | string           | Shipment price before tax                                                          |
|           | tax\_amount            | string           | Tax charged                                                                        |

<h2 id="driver-object-od-order-details-2026-06">Driver Object</h2>

Populated on the order by the courier webhook / polling once a driver is assigned. The whole object is `null` until then — always guard for `null` before reading any nested key. Individual string fields fall back to `""` when the courier does not supply them.

| Parameter               | Type            | Description                                        |
| ----------------------- | --------------- | -------------------------------------------------- |
| name                    | string          | Driver name                                        |
| phone                   | string          | Driver contact number                              |
| photo                   | string          | Driver photo URL                                   |
| rating                  | string          | Driver rating, returned as a string                |
| vehicle.license\_plate  | string          | Vehicle registration number                        |
| vehicle.model           | string          | Vehicle model                                      |
| vehicle.type            | string          | Vehicle type as reported by the courier            |
| coordinates.latitude    | numeric \| null | Latest known driver latitude. `null` when unknown  |
| coordinates.longitude   | numeric \| null | Latest known driver longitude. `null` when unknown |

<h2 id="waypoint-object-od-order-details-2026-06">Waypoint Object</h2>

| Parameter                    | Type           | Description                                                                       |
| ---------------------------- | -------------- | --------------------------------------------------------------------------------- |
| delivery\_id                 | string         | Courier-side delivery identifier for this waypoint                                |
| name                         | string         | Contact name at this waypoint                                                     |
| email                        | string         | Contact email                                                                     |
| address                      | string         | Full composed address. For SG this already includes the leading `#<unit>, `        |
| unit\_number                 | string         | floor/unit as entered.                                                           |
| phone\_number\_country\_code | string         | Phone country calling code (e.g. `60`)                                            |
| phone\_number                | string         | Contact phone number without the country code                                     |
| type                         | int            | `1` = pickup, `2` = dropoff                                                       |
| note                         | string         | Instruction note for the driver at this waypoint                                  |
| pod                          | string \| null | Proof of delivery. `null` until the waypoint is completed                         |
| coordinate                   | object         | `{ latitude, longitude }` of this waypoint                                        |
| packages                     | array          | Parcel/item details for this waypoint — see below. Deleted items are excluded      |

### Package Entry Structure

| Parameter   | Type   | Description                                                     |
| ----------- | ------ | --------------------------------------------------------------- |
| description | string | Item description                                                |
| quantity    | int    | Item quantity                                                   |
| dimensions  | object | Parcel dimensions/weight as submitted at booking time           |

<h2 id="status-codes-od-order-details-2026-06">Status Codes</h2>

| status | status\_text            |
| ------ | ----------------------- |
| 0      | Cancelled by Customer   |
| 1      | Pending                 |
| 2      | Accepted                |
| 3      | In Transit              |
| 4      | Cancelled by Admin      |
| 5      | Cancelled by Driver     |
| 6      | Fulfilled               |
| 7      | Unable to Find Driver   |

---

<h2 id="sample-error-response-od-order-details-2026-06">Sample Error Response</h2>

### 401 – Unauthorized

Returned when the access token does not resolve to an account.

```json
{
    "status_code": 401,
    "request_id": "1770000000000.a1b2c3d4-e5f6-7890-abcd-ef1234567890",
    "message": "Unauthorized Access",
    "data": "Invalid Access Token"
}
```

### 400 – Missing Required Param

Returned when `booking_id` is absent or is not a string.

```json
{
    "status_code": 400,
    "request_id": "1770000000000.a1b2c3d4-e5f6-7890-abcd-ef1234567890",
    "message": "Missing Required Param;",
    "data": {
        "booking_id": "The booking_id field is required."
    }
}
```

### 400 – Order Not Found For This Account

Returned when the booking does not exist, or exists but belongs to another account's wallet.

```json
{
    "status_code": 400,
    "request_id": "1770000000000.a1b2c3d4-e5f6-7890-abcd-ef1234567890",
    "message": "No Order with booking_id 98765 found from this account",
    "data": []
}
```

### 400 – No Wallet Found

Returned when the authenticated account has no wallet.

```json
{
    "status_code": 400,
    "request_id": "1770000000000.a1b2c3d4-e5f6-7890-abcd-ef1234567890",
    "message": "No wallet found for the given account ID",
    "data": []
}
```

<h2 id="code-implementation-od-order-details-2026-06">OnDemand Order Details Code Implementation Examples</h2>

### JavaScript (Fetch API) | PHP (cURL) | Python (requests)

```javascript
const requestData = { booking_id: "EOD-98765" };

fetch('https://api.easyparcel.com/open_api/2026-06/ondemand/details', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': 'Bearer YOUR_ACCESS_TOKEN'
  },
  body: JSON.stringify(requestData)
})
.then(res => res.json())
.then(result => {
  const order = result.data[0];
  if (!order) return console.warn(result.message);

  console.log(order.booking_id, order.status_text);

  if (order.driver) {
    console.log('Driver:', order.driver.name, order.driver.vehicle.license_plate);
  } else {
    console.log('No driver assigned yet');
  }

  order.waypoint.forEach(w => {
    console.log(w.type === 1 ? 'PICKUP' : 'DROPOFF', w.address, w.pod || '(no POD)');
  });
})
.catch(err => console.error(err));
```

```php
<?php
$data = ["booking_id" => "EOD-98765"];

$ch = curl_init('https://api.easyparcel.com/open_api/2026-06/ondemand/details');
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_POST, true);
curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode($data));
curl_setopt($ch, CURLOPT_HTTPHEADER, [
    'Content-Type: application/json',
    'Authorization: Bearer YOUR_ACCESS_TOKEN'
]);
$response = curl_exec($ch);
curl_close($ch);

$result = json_decode($response, true);
$order  = $result['data'][0] ?? null;

if (!$order) {
    echo $result['message'];
} else {
    echo $order['booking_id'] . ' - ' . $order['status_text'] . PHP_EOL;
    if (!empty($order['driver'])) {
        echo 'Driver: ' . $order['driver']['name'] . PHP_EOL;
    }
    foreach ($order['waypoint'] as $w) {
        echo ($w['type'] == 1 ? 'PICKUP  ' : 'DROPOFF ') . $w['address'] . PHP_EOL;
    }
}
?>
```

```python
import requests

url = 'https://api.easyparcel.com/open_api/2026-06/ondemand/details'
headers = {
    'Content-Type': 'application/json',
    'Authorization': 'Bearer YOUR_ACCESS_TOKEN'
}
data = {"booking_id": "EOD-98765"}

result = requests.post(url, json=data, headers=headers).json()
order = result['data'][0] if result['data'] else None

if not order:
    print(result['message'])
else:
    print(order['booking_id'], order['status_text'])

    driver = order.get('driver')
    print('Driver:', driver['name'] if driver else 'not assigned yet')

    for w in order['waypoint']:
        label = 'PICKUP' if w['type'] == 1 else 'DROPOFF'
        print(label, w['address'], w.get('pod') or '(no POD)')
```

<h2 id="best-practices-od-order-details-2026-06">Best Practices for OnDemand Order Details</h2>

1. **Read `data[0]`** – The payload is an array even for a single order; never assume `data` is an object.
2. **Always null-check `driver`** – It stays `null` for `Pending` orders and only fills in once the courier assigns a driver.
3. **Use waypoint `type` numerically** – `1` is pickup and `2` is dropoff; the details endpoint returns the integer code, not the `pickup`/`dropoff` strings used when booking.
