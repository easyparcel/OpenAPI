# Submit Orders

This feature enables users to submit shipment orders. Users are required to fill in the necessary fields to access the shipping service.

## HTTP Request (Submit)

`POST https://api.easyparcel.com/shipment/submit_orders`

## Submit Order Request
### Request Sample

```json
{
    "coupon_codes": [
        "77f39c22-427a-44f1-8bff-e4f3752ba165"
    ],
    "shipment": [
        {
            "service_id": "EP-CS096",
            "collection_date": "2025-05-19",
            "weight": 1.5,
            "height": 5,
            "length": 5,
            "width": 5,
            "item": [
                {
                    "content": "Electronics",
                    "weight": 0.5,
                    "height": 5,
                    "length": 5,
                    "width": 5,
                    "currency_code": "MYR",
                    "value": 50,
                    "quantity": 1
                },
                {
                    "content": "Electronics 2",
                    "weight": 0.5,
                    "height": 5,
                    "length": 5,
                    "width": 5,
                    "currency_code": "MYR",
                    "value": 50,
                    "quantity": 2
                }
            ],
            "sender": {
                "name": "John Doe",
                "company": "ABC Corp",
                "phone_number_country_code": "+60",
                "phone_number": "1126760658",
                "email": "test@easyparcel.com",
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
                "phone_number": "1163042981",
                "email": "test@easyparcel.com",
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
        },
        {
            "service_id": "EP-CS09C",
            "collection_date": "2025-05-19",
            "weight": 1.5,
            "height": 30,
            "length": 40,
            "width": 20,
            "item": [
                {
                    "content": "Electronics",
                    "weight": 1,
                    "height": 30,
                    "length": 40,
                    "width": 20,
                    "currency_code": "MYR",
                    "value": 50,
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
                    "quantity": 1
                }
            ],
            "sender": {
                "name": "John Doe",
                "company": "ABC Corp",
                "phone_number_country_code": "+60",
                "phone_number": "1126760658",
                "email": "test@easyparcel.com",
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
                "phone_number": "1163042981",
                "email": "test@easyparcel.com",
                "address_1": "456 High St",
                "address_2": "Floor 2",
                "postcode": "11950",
                "city": "Bayan Lepas",
                "subdivison_code": "MY-07",
                "country_code": "MY"
            },
            "feature": {
                "sms_tracking": false,
                "email_tracking": true,
                "whatsapp_tracking": true,
                "awb_branding": false
            }
        }
    ]
}
```

### Main Structure

| Parameter | Type    | Required | Description              |
|-----------|---------|----------|--------------------------|
| shipment  | array   | Yes      | Array of shipment orders |

### Shipment Object

| Parameter           | Type        | Required | Description                          | Remarks                                |
|---------------------|-------------|----------|--------------------------------------|----------------------------------------|
| service_id          | string(10)  | Yes      | Service Identification number        | -                                      |
| collection_date     | date        | Yes      | Date to collect the parcel           | Format: YYYY-MM-DD                     |
| customer_reference_no | string    | No       | Customer reference number            | -                                      |
| weight              | double(8,2) | Yes      | Weight of the parcel                 | in KG                                  |
| unit                | string      | No       | Unit of measurement                  | -                                      |
| height              | double(8,2) | Yes      | Height of the parcel                 | in CM                                  |
| length              | double(8,2) | Yes      | Length of the parcel                 | in CM                                  |
| width               | double(8,2) | Yes      | Width of the parcel                  | in CM                                  |
| item                | array       | Yes      | Items in the parcel                  | refer to [item](#items)                |
| sender              | object      | Yes      | Origin of the parcel                 | refer to [sender](#sender)             |
| receiver            | object      | Yes      | Destination of the parcel            | refer to [receiver](#receiver)         |
| feature             | object      | Yes      | Additional service features          | refer to [feature](#feature)           |

### Sender

| Parameter                        | Type      | Required | Description                              | Remarks                                                   |
|----------------------------------|-----------|----------|------------------------------------------|-----------------------------------------------------------|
| name                             | string    | Yes      | Sender's Name                            | -                                                         |
| company                          | string    | No       | Sender's Company                         | -                                                         |
| phone_number_country_code        | string    | Yes      | Country code of the Phone number         | Example: "+60"                                            |
| phone_number                     | string    | Yes      | Sender's phone number                    | -                                                         |
| alternate_phone_number_country_code | string | No       | Country code for alternate phone number  | -                                                         |
| alternate_phone_number           | string    | No       | Sender's alternate phone number          | -                                                         |
| email                            | string    | No       | Sender's email                           | -                                                         |
| address_1                        | string    | Yes      | Sender's address                         | -                                                         |
| address_2                        | string    | No       | Sender's address (continued)             | -                                                         |
| postcode                         | string    | Yes      | Sender's postcode                        | -                                                         |
| city                             | string    | Yes      | Sender's city/town                       | -                                                         |
| subdivison_code                  | string    | No       | Sender's state/province code             | Example: "MY-07"                                          |
| country_code                     | string(2) | Yes      | The origin country of the parcel         | Example: "MY"                                             |
| point_code                       | string    | No       | A unique identifier for sender location  | -                                                         |

### Receiver

| Parameter                        | Type      | Required | Description                              | Remarks                                                   |
|----------------------------------|-----------|----------|------------------------------------------|-----------------------------------------------------------|
| name                             | string    | Yes      | Receiver's Name                          | -                                                         |
| company                          | string    | No       | Receiver's Company                       | -                                                         |
| phone_number_country_code        | string    | Yes      | Country code of the Phone number         | Example: "+60"                                            |
| phone_number                     | string    | Yes      | Receiver's phone number                  | -                                                         |
| alternate_phone_number_country_code | string | No       | Country code for alternate phone number  | -                                                         |
| alternate_phone_number           | string    | No       | Receiver's alternate phone number        | -                                                         |
| email                            | string    | No       | Receiver's email                         | -                                                         |
| address_1                        | string    | Yes      | Receiver's address                       | -                                                         |
| address_2                        | string    | No       | Receiver's address (continued)           | -                                                         |
| postcode                         | string    | Yes      | Receiver's postcode                      | -                                                         |
| city                             | string    | Yes      | Receiver's city/town                     | -                                                         |
| subdivison_code                  | string    | No       | Receiver's state/province code           | Example: "MY-07"                                          |
| country_code                     | string(2) | Yes      | The destination country of the parcel    | Example: "MY"                                             |
| point_code                       | string    | No       | A unique identifier for receiver location| -                                                         |

### Feature

| Parameter          | Type    | Required | Description                                  | Remarks                                     |
|--------------------|---------|----------|----------------------------------------------|---------------------------------------------|
| sms_tracking       | boolean | No       | Enable SMS tracking notifications            | Default: false                              |
| email_tracking     | boolean | No       | Enable email tracking notifications          | Default: false                              |
| whatsapp_tracking  | boolean | No       | Enable WhatsApp tracking notifications       | Default: false                              |
| awb_branding       | object  | No       | Airway bill branding                         | refer to [awb_branding](#awb_branding)      |
| cod                | object  | No       | Cash on Delivery                             | refer to [cod](#cod)                        |

### awb_branding

| Parameter | Type    | Required | Description                                 | Remarks |
|-----------|---------|----------|---------------------------------------------|---------|
| enable    | boolean | Yes      | To enable or disable Airways Bills Branding | -       |

### cod

| Parameter        | Type        | Required | Description                        | Remarks           |
|------------------|-------------|----------|------------------------------------|-------------------|
| cod_amount       | double      | Yes      | Cash on Delivery amount            | -                 |
| cod_currency_code| string      | Yes      | Currency code for COD transaction  | Example: "MYR"    |

### Items

| Parameter       | Type        | Required | Description                              | Remarks                       |
|-----------------|-------------|----------|------------------------------------------|------------------------------ |
| content         | string      | Yes      | Description of the content               | -                             |
| weight          | double(8,2) | Yes      | Weight of the item                       | in KG                         |
| height          | double(8,2) | Yes      | Height of the item                       | in CM                         |
| length          | double(8,2) | Yes      | Length of the item                       | in CM                         |
| width           | double(8,2) | Yes      | Width of the item                        | in CM                         |
| currency_code   | string(3)   | Yes      | The currency code of the item value      | Example: "MYR"                |
| value           | double(8,2) | Yes      | Value of the item                        | -                             |
| quantity        | int         | Yes      | The item quantity                        | -                             |

## Sumbit Order Response
### Successful Response Example
```json
{
    "status_code": 200,
    "message": "2 requests success, 0 request error.",
    "data": [
        {
            "order_details": {
                "order_number": "EI-2601-U8FZW",
                "account_id": 8583757
            },
            "pricing_breakdown": {
                "currency_code": "MYR",
                "total_order_amount": "23.52",
                "total_paid_amount": "23.52",
                "total_tax_amount": "0.00",
                "coupon_redeemed": "0.00"
            },
            "shipments": [
                {
                    "status": "success",
                    "shipment_number": "ES-2601-K8S32",
                    "courier_service": null,
                    "courier": "Aramex",
                    "courier_logo": "https://s3-ap-southeast-1.amazonaws.com/easyparcel-static/Public/source/general/img/couriers/Aramex.jpg",
                    "awb_number": null,
                    "awb_url": null,
                    "tracking_url": null,
                    "weight": 1.5,
                    "height": 5,
                    "length": 5,
                    "width": 5,
                    "pricing_breakdown": {
                        "currency_code": "MYR",
                        "total_paid_amount": "10.25",
                        "shipment_price": "9.80",
                        "shipment_tax_amount": "0.00",
                        "total_features_price": "0.45",
                        "total_features_tax_amount": "0.00",
                        "coupon_redeemed": "0.00"
                    },
                    "sender": {
                        "point_code": null,
                        "name": "John Doe",
                        "phone_number_country_code": "+60",
                        "phone_number": "1126760658",
                        "alternate_phone_number": null,
                        "alternate_phone_number_country_code": null,
                        "email": "test@easyparcel.com",
                        "company_name": "ABC Corp",
                        "address1": "123 Main St",
                        "address2": "Apt 4B",
                        "city": "Lunas",
                        "subdivision_code": "MY-07",
                        "postcode": "10150",
                        "country_code": "MY"
                    },
                    "receiver": {
                        "point_code": null,
                        "name": "Jane Smith",
                        "phone_number": "1163042981",
                        "phone_number_country_code": "+60",
                        "alternate_phone_number": null,
                        "alternate_phone_number_country_code": null,
                        "email": "test@easyparcel.com",
                        "company_name": "XYZ Inc",
                        "address1": "456 High St",
                        "address2": "Floor 2",
                        "city": "Bayan Lepas",
                        "subdivision_code": "MY-07",
                        "postcode": "11950",
                        "country_code": "MY"
                    },
                    "shipment_items": [
                        {
                            "content": "Electronics",
                            "weight": 0.5,
                            "height": 5,
                            "length": 5,
                            "width": 5,
                            "currency_code": "MYR",
                            "value": 50,
                            "quantity": 1
                        },
                        {
                            "content": "Electronics 2",
                            "weight": 0.5,
                            "height": 5,
                            "length": 5,
                            "width": 5,
                            "currency_code": "MYR",
                            "value": 50,
                            "quantity": 2
                        }
                    ],
                    "features": {
                        "cod": null,
                        "insurance_purchase": [
                            {
                                "service_name": "Insure Plus",
                                "insurance_cover_notice": "for lost or damage",
                                "currency_code": "MYR",
                                "charge_amount": "0.00",
                                "total_amount": "0.00",
                                "tax_amount": "0.00"
                            },
                            {
                                "service_name": "Basic Coverage",
                                "insurance_cover_notice": "for lost or damage",
                                "currency_code": "MYR",
                                "charge_amount": "0.00",
                                "total_amount": "0.00",
                                "tax_amount": "0.00"
                            }
                        ],
                        "shipment_tracking_whatsapp": {
                            "message": "Hey there! Your order from John Doe is ready to be collected for delivery soon!\n\nTracking no: null",
                            "phone_country_code": "+60",
                            "phone_number": "1163042981",
                            "currency_code": "MYR",
                            "total_amount": "0.00",
                            "price": "0.20",
                            "tax_amount": "0.00"
                        },
                        "shipment_tracking_sms": {
                            "message": "Your order from John Doe is ready & trackable once courier scans in. Track at EasyParcel with [Placeholder Trackin..] -Powered by EasyParcel",
                            "phone_country_code": "+60",
                            "phone_number": "1163042981",
                            "currency_code": "MYR",
                            "total_amount": "0.00",
                            "price": "0.20",
                            "tax_amount": "0.00"
                        },
                        "shipment_tracking_email": {
                            "email": "test@easyparcel.com",
                            "currency_code": "MYR",
                            "total_amount": "0.00",
                            "price": "0.05",
                            "tax_amount": "0.00"
                        },
                        "shipment_awb_branding": null
                    }
                },
                {
                    "status": "success",
                    "shipment_number": "ES-2601-XV7UN",
                    "courier_service": null,
                    "courier": "DHL eCommerce",
                    "courier_logo": "https://s3-ap-southeast-1.amazonaws.com/easyparcel-static/Public/source/general/img/couriers/DHLeC.jpg",
                    "awb_number": "7227014253232636",
                    "awb_url": "https://app.easyparcel.com/portal/v2/public/label/ES-2601-XV7UN/3941082?format=A4",
                    "tracking_url": "https://app.easyparcel.com/tools/easytrack/details?courier=DHLeC&awb=7227014253232636",
                    "weight": 4,
                    "height": 30,
                    "length": 40,
                    "width": 20,
                    "pricing_breakdown": {
                        "currency_code": "MYR",
                        "total_paid_amount": "13.27",
                        "shipment_price": "13.02",
                        "shipment_tax_amount": "0.00",
                        "total_features_price": "0.25",
                        "total_features_tax_amount": "0.00",
                        "coupon_redeemed": "0.00"
                    },
                    "sender": {
                        "point_code": null,
                        "name": "John Doe",
                        "phone_number_country_code": "+60",
                        "phone_number": "1126760658",
                        "alternate_phone_number": null,
                        "alternate_phone_number_country_code": null,
                        "email": "test@easyparcel.com",
                        "company_name": "ABC Corp",
                        "address1": "123 Main St",
                        "address2": "Apt 4B",
                        "city": "Lunas",
                        "subdivision_code": "MY-07",
                        "postcode": "10150",
                        "country_code": "MY"
                    },
                    "receiver": {
                        "point_code": null,
                        "name": "Jane Smith",
                        "phone_number": "1163042981",
                        "phone_number_country_code": "+60",
                        "alternate_phone_number": null,
                        "alternate_phone_number_country_code": null,
                        "email": "test@easyparcel.com",
                        "company_name": "XYZ Inc",
                        "address1": "456 High St",
                        "address2": "Floor 2",
                        "city": "Bayan Lepas",
                        "subdivision_code": "MY-07",
                        "postcode": "11950",
                        "country_code": "MY"
                    },
                    "shipment_items": [
                        {
                            "content": "Electronics",
                            "weight": 1,
                            "height": 30,
                            "length": 40,
                            "width": 20,
                            "currency_code": "MYR",
                            "value": 50,
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
                            "quantity": 1
                        }
                    ],
                    "features": {
                        "cod": null,
                        "insurance_purchase": [
                            {
                                "service_name": "Insure Plus",
                                "insurance_cover_notice": "for lost or damage",
                                "currency_code": "MYR",
                                "charge_amount": "0.00",
                                "total_amount": "0.00",
                                "tax_amount": "0.00"
                            },
                            {
                                "service_name": "Basic Coverage",
                                "insurance_cover_notice": "for lost or damage",
                                "currency_code": "MYR",
                                "charge_amount": "0.00",
                                "total_amount": "0.00",
                                "tax_amount": "0.00"
                            }
                        ],
                        "shipment_tracking_whatsapp": {
                            "message": "Hey there! Your order from [Sender's Name] is ready to be collected for delivery soon!\n\nTracking no: [Tracking No.]",
                            "phone_country_code": "+60",
                            "phone_number": "1163042981",
                            "currency_code": "MYR",
                            "total_amount": "0.00",
                            "price": "0.20",
                            "tax_amount": "0.00"
                        },
                        "shipment_tracking_sms": null,
                        "shipment_tracking_email": {
                            "email": "test@easyparcel.com",
                            "currency_code": "MYR",
                            "total_amount": "0.00",
                            "price": "0.05",
                            "tax_amount": "0.00"
                        },
                        "shipment_awb_branding": null
                    }
                }
            ]
        }
    ]
}
```

### Successful Response

| Parameter           | Type      | Description                              |
|---------------------|-----------|------------------------------------------|
| status_code         | int       | Status code of the response              |
| message             | string    | Response message                         |
| data                | array     | Array of order results                   |

### Order Details Object

| Parameter           | Type      | Description                               |
|---------------------|-----------|-------------------------------------------|
| order_details       | object    | Details about the order                   |
| pricing             | object    | Pricing information                       |
| shipments           | array     | Array of shipment details                 |

### Order Details

| Parameter           | Type      | Description                               |
|---------------------|-----------|-------------------------------------------|
| order_number        | string    | Order number of the shipment batch        |
| account_id          | string    | Account ID used for the shipment          |

### Pricing

| Parameter           | Type      | Description                               |
|---------------------|-----------|-------------------------------------------|
| currency_code       | string    | Currency used for the shipment            |
| total_amount        | string    | Total cost of all shipments               |
| total_tax_amount    | string    | Total tax amount                          |

### Shipment Object

| Parameter           | Type      | Description                               |
|---------------------|-----------|-------------------------------------------|
| status              | string    | Status of the shipment request            |
| shipment_number     | string    | The unique number of the shipment         |
| courier_service     | string    | Service type selected for shipment        |
| courier             | string    | Name of the courier service               |
| collection_date     | string    | Collection date of the parcel             |
| awb_url             | string    | URL to access the airway bill             |
| awb_number          | string    | The airway bill number                    |
| tracking_url        | string    | URL to track the parcel                   |
| weight              | double    | Weight of the shipment                    |
| height              | double    | Height of the shipment                    |
| length              | double    | Length of the shipment                    |
| width               | double    | Width of the shipment                     |
| pricing_breakdown   | object    | Detailed pricing breakdown                |
| sender              | object    | Sender details                            |
| receiver            | object    | Receiver details                          |
| shipment_items      | array     | Items in the shipment                     |
| features            | object    | Enabled features details                  |

### Pricing Breakdown

| Parameter           | Type      | Description                               |
|---------------------|-----------|-------------------------------------------|
| currency_code       | string    | Currency used for the shipment            |
| total_order_amount        | string    | Total cost of the shipment                |
| shipment_price      | string    | Base price of the shipment                |
| total_tax_amount          | string    | Tax amount                                |
| total_features_price| string    | Total price for additional features       |
| coupon_redeemed| string    | Total amonut deducted using coupon_redeemed       |

### Features

| Parameter              | Type      | Description                            |
|------------------------|-----------|----------------------------------------|
| cod                    | object    | Cash on Delivery details (if enabled)  |
| shipment_tracking_whatsapp | object | WhatsApp tracking details (if enabled) |
| shipment_tracking_sms  | object    | SMS tracking details (if enabled)      |
| shipment_tracking_email| object    | Email tracking details (if enabled)    |

## Error Response

For failed requests, the response includes error details:

| Parameter           | Type      | Description                                |
|---------------------|-----------|--------------------------------------------|
| status_code         | int       | Status code indicating error               |
| message             | string    | Error summary message                      |
| data                | array     | Array of shipment request details          |
| errors              | array     | List of specific error messages            |

---

### Error Response Example

```json
{
    "status_code": 200,
    "message": "1 request success, 1 request error.",
    "data": [
        {
            "order_details": {
                "order_number": "EI-2601-CS99V",
                "account_id": 8583757
            },
            "pricing_breakdown": {
                "currency_code": "MYR",
                "total_order_amount": "12.55",
                "total_paid_amount": "12.55",
                "total_tax_amount": "0.00",
                "coupon_redeemed": "0.00"
            },
            "shipments": [
                {
                    "status": "success",
                    "shipment_number": "ES-2601-U2W24",
                    "courier_service": null,
                    "courier": "Aramex",
                    "courier_logo": "https://s3-ap-southeast-1.amazonaws.com/easyparcel-static/Public/source/general/img/couriers/Aramex.jpg",
                    "awb_number": null,
                    "awb_url": null,
                    "tracking_url": null,
                    "weight": 1.5,
                    "height": 5,
                    "length": 5,
                    "width": 5,
                    "pricing_breakdown": {
                        "currency_code": "MYR",
                        "total_paid_amount": "12.55",
                        "shipment_price": "12.10",
                        "shipment_tax_amount": "0.00",
                        "total_features_price": "0.45",
                        "total_features_tax_amount": "0.00",
                        "coupon_redeemed": "0.00"
                    },
                    "sender": {
                        "point_code": null,
                        "name": "John Doe",
                        "phone_number_country_code": "+60",
                        "phone_number": "1126760658",
                        "alternate_phone_number": null,
                        "alternate_phone_number_country_code": null,
                        "email": "test@easyparcel.com",
                        "company_name": "ABC Corp",
                        "address1": "123 Main St",
                        "address2": "Apt 4B",
                        "city": "Lunas",
                        "subdivision_code": "MY-07",
                        "postcode": "10150",
                        "country_code": "MY"
                    },
                    "receiver": {
                        "point_code": null,
                        "name": "Jane Smith",
                        "phone_number": "1163042981",
                        "phone_number_country_code": "+60",
                        "alternate_phone_number": null,
                        "alternate_phone_number_country_code": null,
                        "email": "test@easyparcel.com",
                        "company_name": "XYZ Inc",
                        "address1": "456 High St",
                        "address2": "Floor 2",
                        "city": "Bayan Lepas",
                        "subdivision_code": "MY-07",
                        "postcode": "11950",
                        "country_code": "MY"
                    },
                    "shipment_items": [
                        {
                            "content": "Electronics",
                            "weight": 0.5,
                            "height": 5,
                            "length": 5,
                            "width": 5,
                            "currency_code": "MYR",
                            "value": 50,
                            "quantity": 1
                        },
                        {
                            "content": "Electronics 2",
                            "weight": 0.5,
                            "height": 5,
                            "length": 5,
                            "width": 5,
                            "currency_code": "MYR",
                            "value": 50,
                            "quantity": 2
                        }
                    ],
                    "features": {
                        "cod": null,
                        "insurance_purchase": [
                            {
                                "service_name": "Insure Plus",
                                "insurance_cover_notice": "for lost or damage",
                                "currency_code": "MYR",
                                "charge_amount": "0.00",
                                "total_amount": "0.00",
                                "tax_amount": "0.00"
                            },
                            {
                                "service_name": "Basic Coverage",
                                "insurance_cover_notice": "for lost or damage",
                                "currency_code": "MYR",
                                "charge_amount": "0.00",
                                "total_amount": "0.00",
                                "tax_amount": "0.00"
                            }
                        ],
                        "shipment_tracking_whatsapp": {
                            "message": "Hey there! Your order from John Doe is ready to be collected for delivery soon!\n\nTracking no: null",
                            "phone_country_code": "+60",
                            "phone_number": "1126760658",
                            "currency_code": "MYR",
                            "total_amount": "0.00",
                            "price": "0.20",
                            "tax_amount": "0.00"
                        },
                        "shipment_tracking_sms": {
                            "message": "Your order from John Doe is ready & trackable once courier scans in. Track at EasyParcel with [Placeholder Trackin..] -Powered by EasyParcel",
                            "phone_country_code": "+60",
                            "phone_number": "1163042981",
                            "currency_code": "MYR",
                            "total_amount": "0.00",
                            "price": "0.20",
                            "tax_amount": "0.00"
                        },
                        "shipment_tracking_email": {
                            "email": "test@easyparcel.com",
                            "currency_code": "MYR",
                            "total_amount": "0.00",
                            "price": "0.05",
                            "tax_amount": "0.00"
                        },
                        "shipment_awb_branding": null
                    }
                },
                {
                    "status": "error",
                    "collection_date": "",
                    "weight": "",
                    "height": "",
                    "length": "",
                    "width": "",
                    "sender": {
                        "point_code": null,
                        "name": "John Doe",
                        "phone_number_country_code": "+60",
                        "phone_number": "1163642281",
                        "alternate_phone_number": null,
                        "alternate_phone_number_country_code": null,
                        "email": "test@easyparcel.com",
                        "company_name": "ABC Corp",
                        "address1": "123 Main St",
                        "address2": "Apt 4B",
                        "city": "",
                        "subdivision_code": "",
                        "postcode": "10150",
                        "country_code": "MY"
                    },
                    "receiver": {
                        "point_code": null,
                        "name": "Jane Smith",
                        "phone_number": "1163642281",
                        "phone_number_country_code": "+60",
                        "alternate_phone_number": null,
                        "alternate_phone_number_country_code": null,
                        "email": "test@easyparcel.com",
                        "company_name": "XYZ Inc",
                        "address1": "456 High St",
                        "address2": "Floor 2",
                        "city": "",
                        "subdivision_code": "",
                        "postcode": "",
                        "country_code": "MY"
                    },
                    "shipment_items": [
                        {
                            "content": "Electronics",
                            "weight": 0.5,
                            "height": 30,
                            "length": 40,
                            "width": 20,
                            "currency_code": "MYR",
                            "value": 50,
                            "quantity": 1,
                            "insurance_purchase": null
                        },
                        {
                            "content": "Electronics 2",
                            "weight": 0.5,
                            "height": 10,
                            "length": 20,
                            "width": 20,
                            "currency_code": "MYR",
                            "value": 50,
                            "quantity": 2,
                            "insurance_purchase": null
                        }
                    ],
                    "features": {
                        "cod": false,
                        "shipment_tracking_whatsapp": false,
                        "shipment_tracking_sms": false,
                        "shipment_tracking_email": false
                    },
                    "errors": [
                        "The receiver postcode field is required "
                    ]
                }
            ]
        }
    ]
}
```
