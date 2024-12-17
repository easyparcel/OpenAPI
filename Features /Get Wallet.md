### Get Wallet
Get Wallet: This features enables users to check their account wallet details/status.

### [Request](#Requested-Parameters)  |  [Return](#Returned-Parameters) 

#### Requested Parameters
Request Sample Code:
```
https://developer.easyparcel.com/wallet
```
#### Returned Parameters

| Returned Parameters | Type      | Description                                     |
| ------------------- | --------- | ----------------------------------------------- |
| id                  | string    | Wallet identification number                    |
| balance             | double    | Balance of the wallet                           |
| currency            | string    | Currency used for the wallet                    |


Return Sample Code:
```
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