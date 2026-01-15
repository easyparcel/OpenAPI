<h1 id="wallet-balance-2025-06">Wallet Balance </h1>

This endpoint allows users to retrieve their current wallet balance and free credit information.

<h2 id="http-request-wallet-2025-06">HTTP Request (Wallet)</h2>

`GET https://api.easyparcel.com/open_api/2025-06/wallet`


<h2 id="request-wallet-parameters-2025-06">Request Wallet Parameters</h2>

This endpoint does not require any request parameters. Authentication is handled through Oauth 2.0 access token.

### Request Sample for Wallet

`No request body required`


<h2 id="response-wallet-parameters-2025-06">Response Wallet Parameters</h2>

### Response Sample for Wallet

```json
{
    "status_code": 200,
    "message": "Success",
    "data": {
        "wallet": [
            {
                "balance": 9999999123.88,
                "currency": "MYR"
            }
        ],
        "free_credit_wallet": [
            {
                "balance": 0,
                "currency": "MYR"
            }
        ]
    }
}
```

### Main Response Structure

| Parameter    | Type    | Description                           |
|--------------|---------|---------------------------------------|
| status_code  | int     | Status code of the response           |
| message      | string  | Response message                      |
| data         | object  | Contains wallet information           |

### Data Object

| Parameter         | Type    | Description                        |
|-------------------|---------|------------------------------------|
| wallet            | array   | Array of wallet balances           |
| free_credit_wallet| array   | Array of free credit balances      |

### Wallet Object

| Parameter    | Type    | Description                           |
|--------------|---------|---------------------------------------|
| balance      | double  | Available balance in the wallet       |
| currency     | string  | Currency code of the balance          |

### Free Credit Wallet Object

| Parameter    | Type    | Description                           |
|--------------|---------|---------------------------------------|
| balance      | double  | Available free credits                |
| currency     | string  | Currency code of the free credits     |



<h2 id="wallet-error-response-2025-06">Error Response for Wallet</h2>

If there's an authentication issue or server error, the API will return an error response:

```json
{
    "status_code": 401,
    "message": "Unauthorized access",
    "data": null
}
```

<h2 id="usage-notes-wallet-2025-06">Usage Notes for Wallet </h2>

1. This endpoint provides the current balance in your EasyParcel wallet, which can be used for shipping services.
2. The response includes both regular wallet balance and free credit balance.
3. Free credits may have expiration dates and usage restrictions that are not included in this response.
4. Multiple currency wallets are supported, though most accounts will only have one currency.
5. The balance is updated in real-time and reflects the current available amount for shipping services.
6. Wallet balances can be topped up through the EasyParcel dashboard or using the top-up API endpoints (if available).
7. Always ensure your account has sufficient balance before submitting shipment orders to avoid processing delays.
