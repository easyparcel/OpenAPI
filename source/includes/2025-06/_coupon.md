<h1 id="coupon-feature-2025-06">Coupon Feature</h1>

The coupon feature allows customers to search for available promo codes and apply them during the shipment order submission. This helps users enjoy discounted rates or special benefits based on current promotional campaigns.


<h2 id="searching-for-coupons-2025-06">Searching for Coupons</h2>

Customers can retrieve a list of available coupon codes using the following endpoint:

<h2 id="http-request-coupon-2025-06"> HTTP Request (Coupon)</h2>

`GET https://api.easyparcel.com/open_api/2025-06/shipment/get_coupon_list`

This will return a list of valid promo codes available to use for the shipment from the user’s account, based on factors such as delivery type, courier, or region.


<h2 id="coupon-request-2025-06">Coupon Request</h2>

Submitting to the Coupon Listing Endpoint based on the submit shipment order endpoint request to get the available coupon for the shipment

### Sample Coupon Listing Request:
```json
{
    "shipment": [
        {
            "service_id": "EP-CS05M",
            "collection_date": "2025-04-20",
            "weight": 2.5,
            "height": 5,
            "length": 6,
            "width": 7,
            "item": [
                {
                    "content": "Electronics 2",
                    "weight": 1.0,
                    "height": 5,
                    "length": 6,
                    "width": 7,
                    "currency_code": "MYR",
                    "value": 20,
                    "quantity": 2
                },
                {
                    "content": "Electronics 1",
                    "weight": 0.5,
                    "height": 5,
                    "length": 6,
                    "width": 7,
                    "currency_code": "MYR",
                    "value": 20,
                    "quantity": 1
                }
            ],
            "sender": {
                "name": "John Doe",
                "company": "ABC Corp",
                "phone_number_country_code": "MY",
                "phone_number": "1263042201",
                "email": "john@easyparcel.com",
                "address_1": "123 Main St",
                "address_2": "Apt 4B",
                "postcode": "11900",
                "city": "Lunas",
                "subdivision_code": "MY-07",
                "country_code": "MY"
            },
            "receiver": {
                "name": "Jane Smith",
                "company": "XYZ Inc",
                "phone_number_country_code": "MY",
                "phone_number": "1169641281",
                "email": "smith@easyparcel.com",
                "address_1": "456 High St",
                "address_2": "Floor 2",
                "postcode": "14000",
                "city": "Bayan Lepas",
                "subdivision_code": "MY-07",
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

<h2 id="coupon-respond-2025-06"> Coupon Respond</h2>

### Coupon Listing API - Response Parameters

### Sample Respone for the courier listing

```json
{
    "status_code": 200,
    "message": "1 coupon(s) available",
    "data": {
        "account_id": 8583757,
        "currency_code": "MYR",
        "coupons": [
            {
                "coupon_code": "d1a1764b-9dcd-4d04-9b5d-8fff28c58db4",
                "title": "RM2 OFF For New Users Only",
                "description": "- Enjoy RM2 OFF on your domestic/international delivery by using this exclusive coupon on EasyParcel. \n- Applicable for all shipment booking on EasyParcel, exclude those orders booked via integrations/API. \n- Valid for one year. \n- Each coupon application will be given a one-off RM2 discount with no minimum spend. \n- This coupon will not be returned when there’s any shipment cancellation. \n- This coupon is strictly not refundable or exchangeable for cash. \n- This coupon will be invalid and will not be replaced once expired. \n- EasyParcel reserves the right to vary and amend any of the above terms and conditions from time to time without prior notice.",
                "discounted_amount": "2.00",
                "discount_rate": "100.00%",
                "valid_from_date": "2026-01-28 13:56:27",
                "valid_to_date": "2027-01-28 13:56:27"
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


### Applying Coupons

During the order submission process (e.g., `/shipment/submit` or `/ondemand/shipment/submit`), customers can apply a valid coupon code by including it in the request body.

### To apply coupon just adding the coupon_codes parameters to the request

### Sample Field in submit orders:

```json
{
    
   "coupon_codes" :["d1a1764b-9dcd-4d04-9b5d-8fff28c58db4"],
   "shipment": [
        {
            // as per the shipment details
        }
 
    ]
}
```

If the coupon is valid and applicable, the discounted amount will be reflected in the final pricing.

Please ensure the coupon is valid and not expired before applying. For additional validation feedback, refer to the response message from the submission endpoint.
