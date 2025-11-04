# Shipment Details

This endpoint allows users to retrieve detailed information about a specific shipment using its shipment number.

## HTTP Request (detail)

`POST https://api.easyparcel.com/open_api/2025-06/shipment/details`

## Shipment Details Request Parameters

| Parameter       | Type    | Required | Description                | Remarks                |
|-----------------|---------|----------|----------------------------|------------------------|
| shipment_number | string  | Yes      | Shipment number to query   | Format: ES-YYMM-XXXXX  |

### Request Sample

```json
{
  "shipment_number": "ES-2504-3WYYP"
}
```


## Shipment Details Return Parameters

### Response Sample

```json
{
    "status_code": 200,
    "message": "success",
    "data": [
        {
            "shipment_number": "ES-2504-3WYYP",
            "order_number": "EI-2504-AK8CK",
            "shipment_details": {
                "weight": 2.5,
                "height": 30,
                "length": 40,
                "width": 20,
                "shipment_status_code": 7,
                "shipment_status": "Schedule In Arrangement",
                "parcels_value": "550",
                "insurance_label": null,
                "awb_number": null,
                "tracking_url": "https://app.easyparcel.com/my/en/track/details/?courier=Celcius Express&awb=null",
                "awb_url": "https://connect.easyparcel.my/?ac=AWBLabel&id=null",
                "coll_date": "2025-05-02 00:00:00"
            },
            "parcel_content": [
                {
                    "content": "Electronics",
                    "weight": "0.50000",
                    "height": 30,
                    "length": 40,
                    "width": 20,
                    "value": 500,
                    "currency_code": "MYR"
                },
                {
                    "content": "Electronics 2",
                    "weight": "0.50000",
                    "height": 10,
                    "length": 20,
                    "width": 20,
                    "value": 50,
                    "currency_code": "MYR"
                }
            ],
            "courier": {
                "courier_name": "Celcius Express Sdn. Bhd.",
                "service_id": "EP-CS0DP",
                "courier_id": "EP-CR0DP",
                "courier_logo": "https://s3-ap-southeast-1.amazonaws.com/easyparcel/Public/source/general/img/couriers/",
                "service_types": "Celcius Express"
            },
            "sender": {
                "name": "John Doe",
                "company_name": "ABC Corp",
                "email": "weikeong.liew@easyparcel.com",
                "contact": "+601163642281",
                "alternative_contact": null,
                "subdivision_code": null,
                "postal_code": "10150",
                "country": "MY",
                "address1": "123 Main St",
                "address2": "Apt 4B",
                "city": "Lunas"
            },
            "receiver": {
                "name": "Jane Smith",
                "company_name": "XYZ Inc",
                "email": "weikeong.liew@easyparcel.com",
                "contact": "+601163642281",
                "alternative_contact": null,
                "subdivision_code": null,
                "postal_code": "11950",
                "country": "MY",
                "address1": "456 High St",
                "address2": "Floor 2",
                "city": "Bayan Lepas"
            },
            "pricing": {
                "currency_code": "MYR",
                "total_price": "27.24",
                "shipment_price": "25.70",
                "tax_price": "1.54",
                "sms_notification": "0.24",
                "email_notification": "0.06",
                "whatsapp_notification": "0.29",
                "awb_branding": null,
                "insurance": null,
                "ddp": null
            }
        }
    ]
}
```

### Main Response Structure

| Parameter    | Type    | Description                           |
|--------------|---------|---------------------------------------|
| status_code  | int     | Status code of the response           |
| message      | string  | Response message                      |
| data         | array   | Array containing the shipment details |

### Shipment Object

| Parameter         | Type    | Description                            |
|-------------------|---------|----------------------------------------|
| shipment_number   | string  | Unique shipment identifier             |
| order_number      | string  | Order number associated with shipment  |
| shipment_details  | object  | Detailed shipment information          |
| parcel_content    | array   | List of items in the shipment          |
| courier           | object  | Courier service information            |
| sender            | object  | Sender information                     |
| receiver          | object  | Receiver information                   |
| pricing           | object  | Detailed pricing breakdown             |

### Shipment Details Object

| Parameter           | Type      | Description                                 |
|---------------------|-----------|---------------------------------------------|
| weight              | double    | Total weight of the shipment                |
| height              | double    | Height of the shipment                      |
| length              | double    | Length of the shipment                      |
| width               | double    | Width of the shipment                       |
| shipment_status_code| int       | Status code of the shipment                 |
| shipment_status     | string    | Human-readable shipment status              |
| parcels_value       | string    | Total value of items in the shipment        |
| insurance_label     | string    | Insurance information (null if not insured) |
| awb_number          | string    | Airway bill number (null if not assigned)   |
| tracking_url        | string    | URL to track the shipment                   |
| awb_url             | string    | URL to access the airway bill               |
| coll_date           | string    | Collection date and time                    |

### Parcel Content Object

| Parameter       | Type      | Description                       |
|-----------------|-----------|-----------------------------------|
| content         | string    | Description of the item           |
| weight          | string    | Weight of the item                |
| height          | int       | Height of the item                |
| length          | int       | Length of the item                |
| width           | int       | Width of the item                 |
| value           | double    | Monetary value of the item        |
| currency_code   | string    | Currency code for the item value  |

### Courier Object

| Parameter       | Type      | Description                            |
|-----------------|-----------|----------------------------------------|
| courier_name    | string    | Full name of the courier company       |
| service_id      | string    | Unique identifier for the service      |
| courier_id      | string    | Unique identifier for the courier      |
| courier_logo    | string    | URL to the courier logo image          |
| service_types   | string    | Type of courier service                |

### Sender Object

| Parameter           | Type      | Description                                |
|---------------------|-----------|--------------------------------------------|
| name                | string    | Name of the sender                         |
| company_name        | string    | Company name of the sender                 |
| email               | string    | Email address of the sender                |
| contact             | string    | Contact number with country code           |
| alternative_contact | string    | Alternative contact number (null if none)  |
| subdivision_code    | string    | State/province code (null if not provided) |
| postal_code         | string    | Postal/ZIP code                            |
| country             | string    | Country code                               |
| address1            | string    | First line of the sender's address         |
| address2            | string    | Second line of the sender's address        |
| city                | string    | City/town of the sender                    |

### Receiver Object

| Parameter           | Type      | Description                                 |
|---------------------|-----------|---------------------------------------------|
| name                | string    | Name of the receiver                        |
| company_name        | string    | Company name of the receiver                |
| email               | string    | Email address of the receiver               |
| contact             | string    | Contact number with country code            |
| alternative_contact | string    | Alternative contact number (null if none)   |
| subdivision_code    | string    | State/province code (null if not provided)  |
| postal_code         | string    | Postal/ZIP code                             |
| country             | string    | Country code                                |
| address1            | string    | First line of the receiver's address        |
| address2            | string    | Second line of the receiver's address       |
| city                | string    | City/town of the receiver                   |

### Pricing Object

| Parameter               | Type      | Description                                      |
|-------------------------|-----------|--------------------------------------------------|
| currency_code           | string    | Currency code for all pricing                    |
| total_price             | string    | Total price of the shipment                      |
| shipment_price          | string    | Base shipping cost                               |
| tax_price               | string    | Tax amount                                       |
| sms_notification        | string    | Price for SMS notification (null if not enabled) |
| email_notification      | string    | Price for email notification (null if not enabled) |
| whatsapp_notification   | string    | Price for WhatsApp notification (null if not enabled) |
| awb_branding            | string    | Price for AWB branding (null if not enabled)     |
| insurance               | string    | Price for insurance (null if not purchased)      |
| ddp                     | string    | Delivered Duty Paid fee (null if not applicable) |


### Error Response

If the shipment is not found or the request is invalid, the API will return an error response:

```json
{
    "status_code": 404,
    "message": "No Order with shipment_number ES-2504-3WYYP found from this account",
    "data": []
}
```

## Usage Notes (detail)

1. This endpoint retrieves comprehensive information about a single shipment.
2. The shipment number must be in the format ES-YYMM-XXXXX (e.g., ES-2504-3WYYP).
3. Values for various fields like awb_number, insurance_label, etc. may be null if they aren't applicable to the shipment's current status.
4. Pricing details provide a complete breakdown of all charges associated with the shipment.
5. The tracking_url can be used to provide tracking information to customers.
