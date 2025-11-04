# Ondemand Coupon

The coupon feature allows customers to search for available promo codes and apply them during the shipment order submission. This helps users enjoy discounted rates or special benefits based on current promotional campaigns.


## HTTP Request (Ondemand coupon list)

Customers can retrieve a list of available coupon codes using the following endpoint:

`GET https://api.easyparcel.com/open_api/2025-06/ondemand/get_coupon_list`

This will return a list of valid promo codes available to use for the shipment from the user’s account, based on factors such as delivery type, courier, or region.


## Ondemand coupon Request

### Submitting to the Coupon Listing Endpoint based on the submit shipment order endpoint request to get the available coupon for the shipment

### Sample Coupon Listing Request:
```json
{
    "origin_country": "MY",
    "ondemand_service_id": "EP-CS09",
    "schedule_pickup_date": "2024-12-10",
    "schedule_pickup_time": "17:35:15",
    "time_zone": "Asia/Kuala_Lumpur",
    "metadata": {
        "quotationId": "3114850556997669249"
    },
    "waypoint": [
        {
            "point": 0,
            "type": "pickup",
            "remark": "1",
            "coordinates": {
                "latitude": 5.342720241204454,
                "longitude": 100.28204988381822
            },
            "item": [
                {
                    "quantity": "1",
                    "description": "1",
                    "dimensions": {
                        "height": "1",
                        "width": "1",
                        "length": "1",
                        "weight": "1"
                    }
                }
            ],
            "shipment_info": {
                "phone_number_country_code": "MY",
                "phone_number": "1278491622",
                "address": "L1 Lobby, Suntec City Tower 1 & 2, 7 Temasek Boulevard, Singapore, 038987",
                "name": "111",
                "email": "as@as.as"
            }
        },
        {
            "point": 1,
            "type": "dropoff",
            "remark": "222",
            "coordinates": {
                "latitude": 5.325513957,
                "longitude": 100.2862732
            },
            "item": [
                {
                    "quantity": "2",
                    "description": "2",
                    "dimensions": {
                        "height": "2",
                        "width": "2",
                        "length": "2",
                        "weight": "2"
                    }
                }
            ],
            "shipment_info": {
                "name": "222",
                "email": "as@as.as",
                "phone_number_country_code": "MY",
                "phone_number": "127491622",
                "address": "Terminal 1 Departure - Changi Airport, 80 Airport Boulevard, Singapore, 819642"
            }
        }
    ]
}
```

## Ondemand Coupon list Response

### Sample Respone for the coupon listing

```json
{
    "status_code": 200,
    "message": "4 coupon(s) available",
    "data": {
        "account_id": 438368,
        "currency_code": "MYR",
        "coupons": [
            {
                "coupon_code": "77f39c22-427a-44f1-8bff-e4f3752ba165",
                "title": "Test Coupon 1",
                "description": "Test ",
                "discounted_amount": "5.01",
                "discount_rate": "20.00%",
                "valid_from_date": "2025-05-12 18:04:33",
                "valid_to_date": "2025-09-14 18:04:33"
            },
            {
                "coupon_code": "10101f8b-1dc5-49e0-b4d3-09c5deb76513",
                "title": "Test Coupon",
                "description": "vvffg",
                "discounted_amount": "2.34",
                "discount_rate": "10.00%",
                "valid_from_date": "2025-05-12 09:43:43",
                "valid_to_date": "2025-07-13 09:43:43"
            },
            {
                "coupon_code": "dfa5109a-2f35-427e-8482-9b0ab65c323f",
                "title": "Test Coupon",
                "description": "vvffg",
                "discounted_amount": "2.10",
                "discount_rate": "10.00%",
                "valid_from_date": "2025-05-12 09:43:43",
                "valid_to_date": "2025-07-13 09:43:43"
            },
            {
                "coupon_code": "ad205174-d93d-4d6a-a5cc-1e989b0292eb",
                "title": "Test Coupon",
                "description": "vvffg",
                "discounted_amount": "1.89",
                "discount_rate": "10.00%",
                "valid_from_date": "2025-05-12 09:43:43",
                "valid_to_date": "2025-07-13 09:43:43"
            }
        ]
    }
}
```

### 🧾 Coupon Listing API - Response Parameters

#### Main Response

| Parameter    | Type   | Description                                             |
|--------------|--------|---------------------------------------------------------|
| status_code  | int    | HTTP status code indicating success or failure          |
| message      | string | Description of the response message                     |
| data         | object | Container for coupon and account details                |

#### `data` Object

| Parameter       | Type    | Description                                           |
|-----------------|---------|-------------------------------------------------------|
| account_id      | int     | The EasyParcel account ID                             |
| currency_code   | string  | Currency in which the discount is offered (e.g., MYR) |
| coupons         | array   | List of coupon objects available for use              |

#### `coupon` Object (Inside `coupons` array)

| Parameter          | Type    | Description                                         |
|--------------------|---------|-----------------------------------------------------|
| coupon_code        | string  | Unique identifier for the coupon                    |
| title              | string  | Title or name of the coupon campaign                |
| description        | string  | Description or note about the coupon                |
| discounted_amount  | string  | Discount value in currency terms                    |
| discount_rate      | string  | Discount in percentage (e.g., "10.00%")             |
| valid_from_date    | string  | Start datetime of coupon validity (UTC format)      |
| valid_to_date      | string  | End datetime of coupon validity (UTC format)        |


### 🧾 Applying Coupons

During the order submission process (e.g., `/shipment/submit` or `/ondemand/shipment/submit`), customers can apply a valid coupon code by including it in the request body.

### To apply coupon just adding the coupon_codes parameters to the request

## Sample Field in submit orders:

```json
{ 
    "coupon_codes":["a186f575-8481-4cf0-80e6-909871eb7e97"],
    "origin_country": "MY",
    "ondemand_service_id": "EP-CS09",
    "schedule_pickup_date": "2024-12-10",
    "schedule_pickup_time": "17:35:15",
    "time_zone": "Asia/Kuala_Lumpur",
    "metadata": {
        "quotationId": "3114850556997669249"
    },
    "waypoint": [
        {
            "point": 0,
            "type": "pickup",
            "remark": "1",
            "coordinates": {
                "latitude": 5.342720241204454,
                "longitude": 100.28204988381822
            },
            "item": [
                {
                    "quantity": "1",
                    "description": "1",
                    "dimensions": {
                        "height": "1",
                        "width": "1",
                        "length": "1",
                        "weight": "1"
                    }
                }
            ],
            "shipment_info": {
                "phone_number_country_code": "MY",
                "phone_number": "1278491622",
                "address": "L1 Lobby, Suntec City Tower 1 & 2, 7 Temasek Boulevard, Singapore, 038987",
                "name": "111",
                "email": "as@as.as"
            }
        },
        {
            "point": 1,
            "type": "dropoff",
            "remark": "222",
            "coordinates": {
                "latitude": 5.325513957,
                "longitude": 100.2862732
            },
            "item": [
                {
                    "quantity": "2",
                    "description": "2",
                    "dimensions": {
                        "height": "2",
                        "width": "2",
                        "length": "2",
                        "weight": "2"
                    }
                }
            ],
            "shipment_info": {
                "name": "222",
                "email": "as@as.as",
                "phone_number_country_code": "MY",
                "phone_number": "127491622",
                "address": "Terminal 1 Departure - Changi Airport, 80 Airport Boulevard, Singapore, 819642"
            }
        }
    ]
}
```

If the coupon is valid and applicable, the discounted amount will be reflected in the final pricing.

Please ensure the coupon is valid and not expired before applying. For additional validation feedback, refer to the response message from the submission endpoint.

