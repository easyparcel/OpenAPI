### Get Wallet
Get Wallet: This features enables users to check their account wallet details/status.

#### [Feature/Endpoints](README.md)  |  [Back to official documentation](../README.md) 

### [Request](#Requested-Parameters)  |  [Return](#Returned-Parameters) 

#### Requested Parameters / Endpoint URL
Request Sample Code:
```
https://api.easyparcel.com/wallet
```
#### Returned Parameters

| Returned Parameters | Type      | Description                                     |
| ------------------- | --------- | ----------------------------------------------- |
| id                  | string    | Wallet identification number                    |
| balance             | double    | Balance of the wallet                           |
| currency            | string    | Currency used for the wallet                    |


Return Sample Code:
``` js
{
    "status_code": 200,
    "message": "Success",
    "data": [
        {
            "id": 3495166,
            "balance": 318.48,
            "currency": "MYR"
        },
        {
            "id": 3495167,
            "balance": 0,
            "currency": "SGD"
        },
        {
            "id": 3495168,
            "balance": 0,
            "currency": "THB"
        },
        {
            "id": 3495169,
            "balance": 0,
            "currency": "IDR"
        },
        {
            "id": 3495170,
            "balance": 0,
            "currency": "USD"
        },
        {
            "id": 3495171,
            "balance": 0,
            "currency": "GBP"
        },
        {
            "id": 3495172,
            "balance": 0,
            "currency": "AUD"
        }
    ]
}
```
<div align="center" style="margin: 2rem 0;">

[![Back to document](https://img.shields.io/badge/Back_to_document-007ACC?style=flat-square)](../README.md)
[![← Previous Paragraph](https://img.shields.io/badge/←_Previous_Paragraph-FF7733?style=flat-square)](/Features/Shipping/4.submit_shipment_orders.md)
[![← OAuth Guide](https://img.shields.io/badge/←_Learn_about_OAuth_Authentication-FF7733?style=flat-square)](/oauth_authentication.md)
[![Order Flow Image →](https://img.shields.io/badge/Next_Section_Order_Flow_Image_→-00CC88?style=flat-square)](https://github.com/easyparcel/OpenAPI/blob/2025-06/Pictures/flow_chart.png)
[![← Country Code Ref](https://img.shields.io/badge/←_References_Country_code-FF7733?style=flat-square)](/References/API_return_status.md)

</div>
