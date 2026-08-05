<h1 id="info-feature-2026-06">Get Information Feature</h1>
Retrieves the authenticated account's profile, addresses, AWB branding availability, and the account-level <b>Portal default settings</b> (`default_settings`). The account is resolved from the access token, so no account identifier is required in the request.

<br>The `default_settings` object contains the merchant's Portal-level default add-on settings (e.g. tracking notification preferences). This field is <b>nullable</b>; if the merchant has never configured any Portal default settings, the API returns `null`.

<h2 id="http-request-2026-06">HTTP Request</h2>

`GET https://api.easyparcel.com/open_api/2026-06/account/get_account_information`

### Authentication
This endpoint requires <b>OAuth 2.0</b> authentication with the following scopes:
- account : read
- wallet : read
### Headers:
```
1. Authorization: Bearer {access_token}
2. Content-Type: application/json
```

<h2 id="account-info-request-parameters-2026-06">Account Info Request</h2>
No request body or query parameters required. The account is determined from the access token.

### Request Example
```
1. GET /2026-06/account/get_account_information HTTP/1.1
2. Host: api.easyparcel.com
3. Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
4. Content-Type: application/json
```

<h2 id="account-info-return-parameters-2026-06">Account Info Response</h2>

### Success Response Example :
#### Success Response (`default_settings` is configured)

```json
{
  "status_code": 200,
  "request_id": "1707830400000.a1b2c3d4-e5f6-7890-abcd-ef1234567890",
  "message": "Success",
  "data": {
    "account": {
      "name": "Acme Trading Sdn Bhd",
      "account_type": "Business"
    },
    "address": {
      "pickup_address": {
        "name": "John Tan",
        "phone_number": "0123456789",
        "alternate_phone_number": "0198765432",
        "email": "john@acme.com",
        "company_name": "Acme Trading Sdn Bhd",
        "address1": "12, Jalan Merdeka",
        "address2": "Taman Sentosa",
        "postcode": "11950",
        "city": "Bayan Lepas",
        "province_code": "PNG",
        "country_code": "MY"
      },
      "billing_address": {
        "name": "John Tan",
        "phone_number": "0123456789",
        "alternate_phone_number": "0198765432",
        "email": "billing@acme.com",
        "company_name": "Acme Trading Sdn Bhd",
        "address1": "12, Jalan Merdeka",
        "address2": "Taman Sentosa",
        "postcode": "11950",
        "city": "Bayan Lepas",
        "province_code": "PNG",
        "country_code": "MY"
      },
      "delivery_address": {}
    },
    "awb_branding": {
      "text": true,
      "banner": false
    },
    "default_settings": {
      "tracking_notifications": {
        "sms": {
          "enable": 1
        },
        "email": {
          "enable": 1
        },
        "whatsapp": {
          "enable": 0
        }
      }
    }
  }
}
```

#### Success Response (`default_settings` is `null`)
```json
{
  "status_code": 200,
  "request_id": "1707830400000.a1b2c3d4-e5f6-7890-abcd-ef1234567890",
  "message": "Success",
  "data": {
    "account": {
      "name": "Jane Personal",
      "account_type": "Personal"
    },
    "address": {
      "pickup_address": {},
      "billing_address": {},
      "delivery_address": {}
    },
    "awb_branding": {
      "text": false,
      "banner": false
    },
    "default_settings": null
  }
}
```

### Error Response Examples:

#### 401 Unauthorized

```json
{
  "status_code": 401,
  "request_id": "1772531409520.3e431a5a-087f-4303-b7b9-f9a1e2368397",
  "message": "Unauthorized Access",
  "data": "Invalid Access Token"
}
```
#### 400 Bad Request

```json
{
  "status_code": 400,
  "request_id": "1707830400000.a1b2c3d4-e5f6-7890-abcd-ef1234567890",
  "message": "Invalid account id, account not found!",
  "data": {}
}
```

### Main Response Structure
| Parameter    | Type    | Description                                             |
|--------------|---------|---------------------------------------------------------|
| status_code  | int     | Status code of the response                             |
| request_id   | string  | A unique Id use to identify the Request of this endpoint|
| message      | string  | Response message                                        |
| data         | array   | Array containing the Account Information                |

### Account Information Object
| Parameter    | Type    | Description                                                |
|--------------|---------|------------------------------------------------------------|
| account      | array   | array that containing the user name and type of account    |
| address      | array   | array that containing the type of the default user address |
| awb_branding | array   | array that containing the AWB branding availability flags  |
| default_settings | array | array that containing the portal-level default settings |

### Account object
| Parameter    | Type    | Description                           |
|--------------|---------|---------------------------------------|
| name         | string | User Name |
| account type | string | Type of the user EasyParcel Account (Personal or Business) |

### Address Object

| Parameter        | Type   | Description                         |
|------------------|--------|-------------------------------------|
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
| unit_no                | string |Unit number (optional)   |
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

### AWB Branding Object

| Name | Type | Description | Example |
|------|------|-------------|---------|
| text | boolean | Returns `true` if the account has a configured AWB branding text (custom text and brand name). | `true` |
| banner | boolean | Returns `true` if the account has a configured AWB branding banner. | `false` |

### Default Settings Object

The account's Portal-level default settings. This object may be `null`. Currently, it contains the `tracking_notifications` settings.

| Name | Type | Description |
|------|------|-------------|
| tracking_notifications | object | Object containing the default tracking notification settings. |
| tracking_notifications.sms.enable | integer | Default setting for Tracking SMS (`1` = enabled, `0` = disabled). |
| tracking_notifications.email.enable | integer | Default setting for Tracking Email (`1` = enabled, `0` = disabled). |
| tracking_notifications.whatsapp.enable | integer | Default setting for Tracking WhatsApp (`1` = enabled, `0` = disabled). |

### Usage Notes

1.  `default_settings` reflects the merchant's Portal add-on defaults. Integrated platforms (e.g. App Hub store connectors) can use this information to detect and reconcile differences between the Portal defaults and a connected store's own add-on settings.
2.  Treat `default_settings` and each nested `tracking_notifications` channel as optional. Always check for `null` values or missing keys before accessing the `enable` field.
3.  The `enable` values are represented as integers (`1` = enabled, `0` = disabled), not booleans.
