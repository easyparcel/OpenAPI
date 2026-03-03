<h1 id="info-feature-2026-03">Get Information Feature</h1>
This feature is allow the customer to get the account detail.(E.g. default pick-up address, dellivery address, billing address)

<h2 id="http-request-2026-03">HTTP Request</h2>

`POST https://api.easyparcel.com/open_api/2026-03/account/get_account_information`

<h2 id="account-info-request-parameters-2026-03">Account Info Request</h2>
**None**

<h2 id="account-info-return-parameters-2026-03">Account Info Response</h2>

###Response Sample
```json
{
    "status_code": 200,
    "request_id": "1772528684225.efb30684-02e6-4f75-b61b-3f2aec7c5a52",
    "message": "Success",
    "data": {
        "account": {
            "name": "Test wk",
            "account_type": "Personal"
        },
        "address": {
            "pickup_address": {
                "name": "Ahmad Firdaus",
                "phone_number": "123456789",
                "alternate_phone_number": null,
                "email": "limwei@gmail.com",
                "company_name": null,
                "address1": "No. 25, Jalan SS15/8A",
                "address2": null,
                "postcode": "47500",
                "city": "Subang Jaya",
                "province_code": "MY-10",
                "country_code": "MY"
            },
            "billing_address": {
                "name": "John",
                "phone_number": "167891234",
                "alternate_phone_number": null,
                "email": "john@gmail.com",
                "company_name": null,
                "address1": "Unit 3-12, Block B",
                "address2": "Pusat Komersial Melawati",
                "postcode": "53100",
                "city": "Kuala Lumpur",
                "province_code": "MY-14",
                "country_code": "MY"
            },
            "delivery_address": {
                "name": "John",
                "phone_number": "167891234",
                "alternate_phone_number": null,
                "email": "john@gmail.com",
                "company_name": null,
                "address1": "Unit 3-12, Block B,",
                "address2": "Pusat Komersial Melawati",
                "postcode": "53100",
                "city": "Kuala Lumpur",
                "province_code": "MY-14",
                "country_code": "MY"
            }
        }
    }
}
```

### Main Response Structure
| Parameter    | Type    | Description                           |
|--------------|---------|---------------------------------------|
| status_code  | int     | Status code of the response           |
| request_id   | string  | A unique Id use to identify the Request of this endpoint|
| message      | string  | Response message                      |
| data | array | Array containing the Account Information |

### Account Information Object
| Parameter    | Type    | Description                           |
|--------------|---------|---------------------------------------|
| account | array | array that containing the user name and type of account |
| address | array | array that containing the type of the default user address |

### Account object
| Parameter    | Type    | Description                           |
|--------------|---------|---------------------------------------|
| name | string | User Name |
| account type | string | Type of the user EasyParcel Account (Personal or Business) |

### Address Object

| Parameter        | Type   | Description                         |
|-----------------|--------|-------------------------------------|
| pickup_address   | object | Sender / pickup address details     |
| billing_address  | object | Billing address details             |
| delivery_address | object | Receiver / delivery address details |


### Pickup Address Object

| Parameter               | Type   | Description                         |
|------------------------|--------|-------------------------------------|
| name                   | string | Sender full name                    |
| phone_number           | string | Sender contact number               |
| alternate_phone_number | string | Sender alternate contact number     |
| email                  | string | Sender email address                |
| company_name           | string | Sender company name (optional)      |
| address1               | string | Primary address line                |
| address2               | string | Secondary address line (optional)   |
| postcode               | string | Postal code                         |
| city                   | string | City name                           |
| province_code          | string | State code (ISO format, e.g. MY-10) |
| country_code           | string | Country code (ISO format, e.g. MY)  |


### Billing Address Object

| Parameter               | Type   | Description                         |
|------------------------|--------|-------------------------------------|
| name                   | string | Billing person name                 |
| phone_number           | string | Billing contact number              |
| alternate_phone_number | string | Billing alternate contact number    |
| email                  | string | Billing email address               |
| company_name           | string | Billing company name (optional)     |
| address1               | string | Primary address line                |
| address2               | string | Secondary address line (optional)   |
| postcode               | string | Postal code                         |
| city                   | string | City name                           |
| province_code          | string | State code (ISO format)             |
| country_code           | string | Country code (ISO format)           |


### Delivery Address Object

| Parameter               | Type   | Description                         |
|------------------------|--------|-------------------------------------|
| name                   | string | Receiver full name                  |
| phone_number           | string | Receiver contact number             |
| alternate_phone_number | string | Receiver alternate contact number   |
| email                  | string | Receiver email address              |
| company_name           | string | Receiver company name (optional)    |
| address1               | string | Primary address line                |
| address2               | string | Secondary address line (optional)   |
| postcode               | string | Postal code                         |
| city                   | string | City name                           |
| province_code          | string | State code (ISO format)             |
| country_code           | string | Country code (ISO format)           |

### Error Response
If the account is not found or the request is invalid, the API will return an error response:
```json
{
    "status_code": 401,
    "request_id": "1772531409520.3e431a5a-087f-4303-b7b9-f9a1e2368397",
    "message": "Unauthorized Access",
    "data": "Invalid Access Token"
}
```

<h2 id="usage-notes-detail-2026-03">Usage Note</h2>
1. This endpoint retrieves the user account information for the EasyParcel account.    

2. It returns details such as the user’s name, email, contact numbers, company name, and default addresses (pickup, billing, delivery).

3. This endpoint is useful for displaying or pre-filling user information when creating shipments or managing account settings.  





