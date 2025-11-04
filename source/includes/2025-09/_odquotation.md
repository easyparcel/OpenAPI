# Ondmeand Quotation

## Ondemand Quotation Overview

This feature enables users to obtain on-demand shipment quotations from all courier companies available on the EasyParcel platform. Users need to provide sender and receiver addresses and waypoint information to retrieve shipment quotations. The response includes available courier services, transportation type, pricing details, and optional add-on features.


## HTTP Request (Ondemand Quotation)

`POST https://api.easyparcel.com/open_api/2025-06/ondemand/quotations`

## Ondemand Quotation Request Parameters 

### Request Sample

```json
{
  "schedule_pickup_date": "2024-11-30",
  "schedule_pickup_time": "11:48:35",
  "timezone": "Asia/Kuala_Lumpur",
  "waypoint": [
    {
      "coordinates": {
        "latitude": 5.342720241204454,
        "longitude": 100.28204988381822
      },
      "address": "Kawasan Mendaki Bukit Jambul, Lintang Bukit Jambul 1, Bukit Jambul Indah, Bayan Lepas, Mukim 13 Paya Terubong, 11900, Timur Laut, Pulau Pinang, Malaysia",
      "type": "pickup"
    },
    {
      "coordinates": {
        "latitude": 5.325513957,
        "longitude": 100.2862732
      },
      "address": "Suntech @ Penang Cybercity, 1, Lintang Mayang Pasir 3, Bandar Bayan Baru, Bayan Lepas, Mukim 12 Bayan Lepas, 11950, Barat Daya, Pulau Pinang, Malaysia",
      "type": "dropoff"
    }
  ]
}
```

### Main Structure

| Parameter                           | Type    | Required | Description                        | Remarks            |
| ----------------------------------- | ------- | -------- | ---------------------------------- | ------------------ |
| schedule\_pickup\_date              | string  | No       | Scheduled pickup date (YYYY-MM-DD) | -                  |
| schedule\_pickup\_time              | string  | No       | Scheduled pickup time (HH\:MM\:SS) | -                  |
| timezone                            | string  | No       | Pickup timezone                    | -                  |
| waypoint                            | array   | Yes      | List of pickup and dropoff points  | Minimum 2 required |
| waypoint\[\*].coordinates.latitude  | numeric | Yes      | Location latitude                  | -                  |
| waypoint\[\*].coordinates.longitude | numeric | Yes      | Location longitude                 | -                  |
| waypoint\[\*].address               | string  | No       | Full address of the location       | -                  |
| waypoint\[\*].type                  | string  | Yes      | Either `pickup` or `dropoff`       | -                  |


## Ondemand Quotation Response Parameters


### Sample Response

Refer to the full JSON response you provided in your message for all details on courier quotations including Lalamove and PandaGo examples with their respective vehicle types, prices, weight and dimension limits.

```json
{
    "status_code": 200,
    "message": "",
    "data": [
        {
            "status": "success",
            "input": {
                "schedule_pickup_date": "2024-11-30",
                "schedule_pickup_time": "11:48:35",
                "timezone": "Asia/Kuala_Lumpur",
                "waypoint": [
                    {
                        "coordinates": {
                            "latitude": 5.342720241204454,
                            "longitude": 100.28204988381822
                        },
                        "address": "Kawasan Mendaki Bukit Jambul, Lintang Bukit Jambul 1, Bukit Jambul Indah, Bayan Lepas, Mukim 13 Paya Terubong, 11900, Timur Laut, Pulau Pinang, Malaysia",
                        "type": "pickup"
                    },
                    {
                        "coordinates": {
                            "latitude": 5.325513957,
                            "longitude": 100.2862732
                        },
                        "address": "Suntech @ Penang Cybercity, 1, Lintang Mayang Pasir 3, Bandar Bayan Baru, Bayan Lepas, Mukim 12 Bayan Lepas, 11950, Barat Daya, Pulau Pinang, Malaysia",
                        "type": "dropoff"
                    }
                ]
            },
            "quotations": [
                {
                    "metadata": {
                        "quotationId": "3214761490129490315"
                    },
                    "courier": {
                        "service_id": "EP-CS0I",
                        "courier_name": "Lalamove",
                        "img_courier": "https://s3-ap-southeast-1.amazonaws.com/easyparcel/Public/source/general/img/couriers/lalamove.svg"
                    },
                    "transport": {
                        "transportation_type": "Car",
                        "durations": "3mins",
                        "parcel_type_support": "Parcel",
                        "weight_limit": "40kg",
                        "dimension": "50cmx50cmx50cm"
                    },
                    "pricing": {
                        "total_amount": "5.65",
                        "currency": "MYR"
                    }
                },
                {
                    "metadata": {
                        "quotationId": "3214762583542600039"
                    },
                    "courier": {
                        "service_id": "EP-CS0F",
                        "courier_name": "Lalamove",
                        "img_courier": "https://s3-ap-southeast-1.amazonaws.com/easyparcel/Public/source/general/img/couriers/lalamove.svg"
                    },
                    "transport": {
                        "transportation_type": "Bike",
                        "durations": "3mins",
                        "parcel_type_support": "Parcel",
                        "weight_limit": "10kg",
                        "dimension": "30cmx30cmx30cm"
                    },
                    "pricing": {
                        "total_amount": "4.71",
                        "currency": "MYR"
                    }
                },
                {
                    "metadata": {
                        "quotationId": "3214762583542600040"
                    },
                    "courier": {
                        "service_id": "EP-CS09",
                        "courier_name": "Lalamove",
                        "img_courier": "https://s3-ap-southeast-1.amazonaws.com/easyparcel/Public/source/general/img/couriers/lalamove.svg"
                    },
                    "transport": {
                        "transportation_type": "4X4",
                        "durations": "3mins",
                        "parcel_type_support": "Ideal for small fridge, washing machine, bike, 1-seater sofa",
                        "weight_limit": "250kg",
                        "dimension": "120cmx90cmx90cm"
                    },
                    "pricing": {
                        "total_amount": "18.82",
                        "currency": "MYR"
                    }
                },
                {
                    "metadata": {
                        "quotationId": "3214761490129490316"
                    },
                    "courier": {
                        "service_id": "EP-CS05",
                        "courier_name": "Lalamove",
                        "img_courier": "https://s3-ap-southeast-1.amazonaws.com/easyparcel/Public/source/general/img/couriers/lalamove.svg"
                    },
                    "transport": {
                        "transportation_type": "Large Van",
                        "durations": "3mins",
                        "parcel_type_support": "Ideal for washing machine, sofa, treadmill , large parcels",
                        "weight_limit": "800kg",
                        "dimension": "270cmx130cmx120cm"
                    },
                    "pricing": {
                        "total_amount": "45.18",
                        "currency": "MYR"
                    }
                },
                {
                    "metadata": {
                        "quotationId": "3214761490129490317"
                    },
                    "courier": {
                        "service_id": "EP-CS0G",
                        "courier_name": "Lalamove",
                        "img_courier": "https://s3-ap-southeast-1.amazonaws.com/easyparcel/Public/source/general/img/couriers/lalamove.svg"
                    },
                    "transport": {
                        "transportation_type": "Lorry 10-ft",
                        "durations": "3mins",
                        "parcel_type_support": "Ideal for queen size bed, fridge, 3-seater sofa, wardrobe",
                        "weight_limit": "1000kg",
                        "dimension": "290cmx150cmx150cm"
                    },
                    "pricing": {
                        "total_amount": "64.00",
                        "currency": "MYR"
                    }
                },
                {
                    "metadata": {
                        "quotationId": "3214762583542600041"
                    },
                    "courier": {
                        "service_id": "EP-CS0M",
                        "courier_name": "Lalamove",
                        "img_courier": "https://s3-ap-southeast-1.amazonaws.com/easyparcel/Public/source/general/img/couriers/lalamove.svg"
                    },
                    "transport": {
                        "transportation_type": "Lorry 14-ft",
                        "durations": "3mins",
                        "parcel_type_support": "Ideal for king size bed, large fridge, 3-seater sofa, wardro",
                        "weight_limit": "2500kg",
                        "dimension": "420cmx200cmx200cm"
                    },
                    "pricing": {
                        "total_amount": "128.00",
                        "currency": "MYR"
                    }
                },
                {
                    "metadata": {
                        "quotationId": "3214761490129490318"
                    },
                    "courier": {
                        "service_id": "EP-CS0Y",
                        "courier_name": "Lalamove",
                        "img_courier": "https://s3-ap-southeast-1.amazonaws.com/easyparcel/Public/source/general/img/couriers/lalamove.svg"
                    },
                    "transport": {
                        "transportation_type": "Van",
                        "durations": "3mins",
                        "parcel_type_support": "Ideal for small fridge, washing machine, bike, 1-seater sofa",
                        "weight_limit": "500kg",
                        "dimension": "170cmx100cmx120cm"
                    },
                    "pricing": {
                        "total_amount": "16.00",
                        "currency": "MYR"
                    }
                }
            ]
        }
    ]
}
```
### Main Structure

| Parameter    | Type   | Description                      |
| ------------ | ------ | -------------------------------- |
| status\_code | int    | HTTP status code                 |
| message      | string | Status message                   |
| data         | array  | List of quotations with metadata |

### Data Object Structure

| Parameter  | Type   | Description                |
| ---------- | ------ | -------------------------- |
| status     | string | Status of the request      |
| input      | object | Echo of submitted input    |
| quotations | array  | List of courier quotations |

### Quotation Entry Structure

| Section   | Parameter             | Type   | Description                      |
| --------- | --------------------- | ------ | -------------------------------- |
| metadata  | quotationId           | string | Unique quotation ID              |
| courier   | service\_id           | string | Service ID                       |
|           | courier\_name         | string | Courier name                     |
|           | img\_courier          | string | Courier logo URL                 |
| transport | transportation\_type  | string | Transport type (e.g., Bike, Car) |
|           | durations             | string | Estimated delivery time          |
|           | parcel\_type\_support | string | Parcel suitability description   |
|           | weight\_limit         | string | Weight limit                     |
|           | dimension             | string | Max parcel dimension             |
| pricing   | total\_amount         | string | Quotation price                  |
|           | currency              | string | Currency (e.g., MYR)             |


---

### Sample Error Response

```json
{
  "status_code": 200,
  "message": "0 requests success, 3 request error.",
  "data": [
    {
      "status": "error",
      "input": { ... },
      "errors": [
        "The receiver postcode field is required"
      ]
    },
  ]
}
```


## Code Implementation Examples

### JavaScript (Fetch API) | PHP (cURL) | Python (requests)

```javascript
const requestData = {
  schedule_pickup_date: "2024-11-30",
  schedule_pickup_time: "11:48:35",
  timezone: "Asia/Kuala_Lumpur",
  waypoint: [
    { type: "pickup", coordinates: { latitude: 5.34, longitude: 100.28 } },
    { type: "dropoff", coordinates: { latitude: 5.32, longitude: 100.28 } }
  ]
};

fetch('https://api.easyparcel.com/open_api/2025-06/ondemand/quotations', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': 'Bearer YOUR_ACCESS_TOKEN'
  },
  body: JSON.stringify(requestData)
})
.then(res => res.json())
.then(data => console.log(data))
.catch(err => console.error(err));
```


```php
<?php
$data = [
    "schedule_pickup_date" => "2024-11-30",
    "schedule_pickup_time" => "11:48:35",
    "timezone" => "Asia/Kuala_Lumpur",
    "waypoint" => [
        ["type" => "pickup", "coordinates" => ["latitude" => 5.34, "longitude" => 100.28]],
        ["type" => "dropoff", "coordinates" => ["latitude" => 5.32, "longitude" => 100.28]]
    ]
];

$ch = curl_init('https://api.easyparcel.com/open_api/2025-06/ondemand/quotations');
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_POST, true);
curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode($data));
curl_setopt($ch, CURLOPT_HTTPHEADER, [
    'Content-Type: application/json',
    'Authorization: Bearer YOUR_ACCESS_TOKEN'
]);
$response = curl_exec($ch);
curl_close($ch);
echo $response;
?>
```


```python
import requests

url = 'https://api.easyparcel.com/open_api/2025-06/ondemand/quotations'
headers = {
    'Content-Type': 'application/json',
    'Authorization': 'Bearer YOUR_ACCESS_TOKEN'
}
data = {
    "schedule_pickup_date": "2024-11-30",
    "schedule_pickup_time": "11:48:35",
    "timezone": "Asia/Kuala_Lumpur",
    "waypoint": [
        {"type": "pickup", "coordinates": {"latitude": 5.34, "longitude": 100.28}},
        {"type": "dropoff", "coordinates": {"latitude": 5.32, "longitude": 100.28}}
    ]
}

response = requests.post(url, json=data, headers=headers)
print(response.json())
```


## Best Practices For Ondemand Quotation

1. **Input Validation** – Validate all fields before API call.
2. **Sorting Quotations** – Sort by total amount for better user experience.
3. **Optional Features** – Allow users to toggle extras like insurance or SMS alerts.
4. **Display Info** – Always show courier logos, transport type, and delivery time.


