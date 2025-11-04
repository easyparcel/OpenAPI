# Coupon Feature

The coupon feature allows customers to search for available promo codes and apply them during the shipment order submission. This helps users enjoy discounted rates or special benefits based on current promotional campaigns.


### 🔍 Searching for Coupons

Customers can retrieve a list of available coupon codes using the following endpoint:

### HTTP Request (coupon)

`GET https://api.easyparcel.com/open_api/2025-06/shipment/get_coupon_list`

This will return a list of valid promo codes available to use for the shipment from the user’s account, based on factors such as delivery type, courier, or region.


## Coupon Request

### Submitting to the Coupon Listing Endpoint based on the submit shipment order endpoint request to get the available coupon for the shipment

### Sample Coupon Listing Request:
```json
{
    "shipment": [
        {
            "service_id": "EP-CS05M",
            "collection_date": "2025-05-19",
            "weight": 2.5,
            "height": 30,
            "length": 40,
            "width": 20,
            "item": [
                {
                    "content": "Electronics",
                    "weight": 0.5,
                    "height": 30,
                    "length": 40,
                    "width": 20,
                    "currency_code": "MYR",
                    "value": 500,
                    "quantity": 1
                },
                {
                    "content": "Electronics 2",
                    "weight": 0.5,
                    "height": 10,
                    "length": 20,
                    "width": 20,
                    "currency_code": "MYR",
                    "value": 50,
                    "quantity": 2
                }
            ],
            "sender": {
                "name": "John Doe",
                "company": "ABC Corp",
                "phone_number_country_code": "+60",
                "phone_number": "1163642281",
                "email": "weikeong.liew@easyparcel.com",
                "address_1": "123 Main St",
                "address_2": "Apt 4B",
                "postcode": "10150",
                "city": "Lunas",
                "subdivison_code": "MY-07",
                "country_code": "MY"
            },
            "receiver": {
                "name": "Jane Smith",
                "company": "XYZ Inc",
                "phone_number_country_code": "+60",
                "phone_number": "1163642281",
                "email": "weikeong.liew@easyparcel.com",
                "address_1": "456 High St",
                "address_2": "Floor 2",
                "postcode": "11950",
                "city": "Bayan Lepas",
                "subdivison_code": "MY-07",
                "country_code": "MY"
            },
            "feature": {
                "sms_tracking": true,
                "email_tracking": true,
                "whatsapp_tracking": true,
                "awb_branding": false
            }
        }
    ]
}
```


## Coupon Respond

### 🧾 Coupon Listing API - Response Parameters

### Sample Respone for the courier listing

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

### Main Response

| Parameter    | Type   | Description                                             |
|--------------|--------|---------------------------------------------------------|
| status_code  | int    | HTTP status code indicating success or failure          |
| message      | string | Description of the response message                     |
| data         | object | Container for coupon and account details                |

### `data` Object

| Parameter       | Type    | Description                                           |
|-----------------|---------|-------------------------------------------------------|
| account_id      | int     | The EasyParcel account ID                             |
| currency_code   | string  | Currency in which the discount is offered (e.g., MYR) |
| coupons         | array   | List of coupon objects available for use              |

### `coupon` Object (Inside `coupons` array)

| Parameter          | Type    | Description                                         |
|--------------------|---------|-----------------------------------------------------|
| coupon_code        | string  | Unique identifier for the coupon                    |
| title              | string  | Title or name of the coupon campaign                |
| description        | string  | Description or note about the coupon                |
| discounted_amount  | string  | Discount value in currency terms                    |
| discount_rate      | string  | Discount in percentage (e.g., "10.00%")             |
| valid_from_date    | string  | Start datetime of coupon validity (UTC format)      |
| valid_to_date      | string  | End datetime of coupon validity (UTC format)        |

---


### 🧾 Applying Coupons

During the order submission process (e.g., `/shipment/submit` or `/ondemand/shipment/submit`), customers can apply a valid coupon code by including it in the request body.

### To apply coupon just adding the coupon_codes parameters to the request

### Sample Field in submit orders:

```json
{
    
   "coupon_codes" :["5f710742-c649-45b7-83d6-af733651f892"],
   "shipment": [
        {
            // as per the shipment details
        }
 
    ]
}
```

If the coupon is valid and applicable, the discounted amount will be reflected in the final pricing.

Please ensure the coupon is valid and not expired before applying. For additional validation feedback, refer to the response message from the submission endpoint.
