<h1 id="Malaysia-E-invoice-2026-03"><span style="color: blue;">Malaysia E-Invoice</span></h1>
<img width="512" height="512" alt="6VqK00VjOdMarAeGI9gkpLNU1lwkBJ" src="https://github.com/user-attachments/assets/006a895f-8823-4e08-aa28-f6524a38f2f9" />       

EasyParcel’s e-Invoice feature is an integrated solution with Lembaga Hasil Dalam Negeri Malaysia (LHDN) MyInvois that allows you to generate, validate, and store your e-Invoices directly after order fulfillment using the EasyParcel OpenAPI integration. 

<h2 id="Setup-Malaysia-E-invoice-2026-03">Setup MyInvois in EasyParcel</h2>

Before starting development, please ensure the e-Invoice feature is enabled in your account via the 
[Developer Hub](https://developer.easyparcel.com/#nav_Individual_EPRateCheckingBulk).

Next, follow the official guidelines provided by Lembaga Hasil Dalam Negeri Malaysia (LHDN) to configure your MyInvois portal and add EasyParcel as an intermediary.

This step is required to allow EasyParcel to submit and manage e-Invoices on your behalf:        

First, you may select your existing app by clicking Settings, or open a new app that you would like to enable the Malaysia e-Invoice feature with EasyParcel.
<img width="1237" height="500" alt="Screenshot 2026-03-19 at 12 00 08 PM" src="https://github.com/user-attachments/assets/8f9a90e7-2f7d-4808-a336-b234d528b2d6" />


Second, Find the **Malaysia E-Invois** and click the status become **Enable**
<img width="1138" height="500" alt="Screenshot 2026-03-17 at 5 48 57 PM" src="https://github.com/user-attachments/assets/2273736c-8c5b-431f-b587-840371a9a6ce" />

Third, follow the steps provided in the diagram or on your side to complete the setup.   
<img width="1051" height="500" alt="Screenshot 2026-03-17 at 5 49 18 PM" src="https://github.com/user-attachments/assets/67165885-a283-4aba-9d5c-baaaa58d7aa7" />

<h2 id="Verify-Malaysia-E-invoice-2026-03">Verify Malaysia E-Invoice Access</h2>
To verify your MyInvois account access status: if the endpoint returns Invalid, please check the intermediary configured in MyInvois. Run this endpoint and ensure your MyInvois account access status is Valid before submitting an e-Invoice.

### Endpoint

'POST https://api.easyparcel.com/open_api/2026-03/einvoice/malaysia/verify_access'

### Example request

```json
{
    "tin_no": "IG900000000",
    "id_no": "201201000000",
    "id_type": "BRN"
}
```

### Request Body

| Field   | Type   | Required | Description |
|---------|--------|----------|-------------|
| tin_no  | string | Yes      | Tax Identification Number. |
| id_no   | string | Yes      | Document number corresponding to `id_type` (e.g. NRIC, Passport, BRN, or Army ID). When `id_type` is BRN, this is the Business Registration Number. |
| id_type | string | Yes      | Identity document type. Must be one of: `NRIC`, `PASSPORT`, `BRN`, `ARMY`. |

### Response 

### Open API – success (200)

```json
{
    "status_code": 200,
    "request_id": "1234567890.uuid",
    "message": "Account has been verified",
    "data": {
        "status": "success"
    }
}
```

### Open API – failure (400)

```json
{
    "status_code": 400,
    "request_id": "1234567890.uuid",
    "message": "E-invoice candidate authentication failed, please follow the documentation to add Intermediary on MyInvoice Portal",
    "data": {
        "status": "error"
    }
}
```

<h2 id="Submit-Malaysia-E-invoice-2026-03">Submit Malaysia E-Invoice</h2>
This API endpoint allows you to submit Malaysia e-invoices in bulk to the LHDN (Lembaga Hasil Dalam Negeri) e-invoice system. The endpoint processes multiple invoices in a single request, with individual validation for each invoice item.

<h2 id="Http-Request-Malaysia-E-invoice-2026-03">HTTP Request(Malaysia MyInvois)</h2>

### Endpoint

`POST https://api.easyparcel.com/open_api/2026-03/einvoice/malaysia/submit`

### Header

`
Authorization: Bearer {access_token}
Content-Type: application/json
`

<h2 id="Request-Malaysia-E-invoice-2026-03">Malaysia Invois Request</h2>

### Example Request 

```json
{
    "tin_no": "IG12345678901",
    "id_no": "123456789",
    "id_type": "BRN",
    "sst_no": "A12-3456-78901234",
    "company_name": "ABC Sdn. Bhd.",
    "company_phone": "+60123456789",
    "msic_code": "63120",
    "business_nature": "OPERATING A WEB-BASED PARCEL CONSOLIDATOR",
    "address_line_1": "1-10-05, Suntech @ Penang Cybercity",
    "city": "Pulau Pinang",
    "postcode": "11950",
    "state_code": "07",
    "bulk": [
        {
            "invoice_no": "EI-2601-ZZHKB",
            "invoice_issue_date": "2024-01-15",
            "invoice_issue_time": "14:30:00",
            "order_currency": "MYR",
            "total_discount_value": 10.00,
            "items": [
                {
                    "description": "Shipping Services - Order #12345",
                    "quantity": 1,
                    "amount": 100.00,
                    "tax_amount": 6.00
                }
            ]
        },
        {
            "invoice_no": "EI-2601-ZZHKC",
            "invoice_issue_date": "2024-01-15",
            "invoice_issue_time": "15:45:00",
            "order_currency": "MYR",
            "items": [
                {
                    "description": "Express Delivery - Order #12346",
                    "quantity": 1,
                    "amount": 200.00,
                    "tax_amount": 12.00
                },
                {
                    "description": "Insurance - Order #12346",
                    "quantity": 1,
                    "amount": 50.50,
                    "tax_amount": 3.03
                }
            ]
        }
    ]
}
```

### Request Body Fields

| Field            | Type   | Required | Description |
|------------------|--------|----------|-------------|
| tin_no           | string | Yes      | Tax Identification Number. |
| id_no            | string | Yes      | Document number corresponding to `id_type` (e.g. NRIC number, Passport number, BRN, or Army ID). When `id_type` is BRN, this is the Business Registration Number. |
| id_type          | string | Yes      | Identity document type. Must be one of: `NRIC`, `PASSPORT`, `BRN`, `ARMY`. |
| sst_no           | string | No       | Sales and Service Tax number (optional). |
| company_name     | string | Yes      | Company registered name. |
| company_phone    | string | Yes      | Company contact phone. |
| msic_code        | string | Yes      | Malaysian Standard Industrial Classification code. |
| business_nature  | string | Yes      | Description of business nature. |
| address_line_1   | string | Yes      | Company address line 1. |
| city             | string | Yes      | City name. |
| postcode         | string | Yes      | Postal code. |
| state_code       | string | Yes      | State code (2-digit, e.g. "07" for Penang). |
| bulk             | array  | Yes      | Array of invoice objects (see below). |



### Bulk array item (each invoice)

| Field                 | Type   | Required | Description |
|-----------------------|--------|----------|-------------|
| invoice_no            | string | Yes      | Invoice number. |
| invoice_issue_date    | string | Yes      | Date in `YYYY-MM-DD` format, must be UTC timezone. |
| invoice_issue_time    | string | Yes      | Time in `HH:mm:ss` format, must be UTC timezone (the system automatically appends `Z`). |
| order_currency        | string | Yes      | Must be `"MYR"` for Malaysia. |
| total_discount_value  | number | No       | Total discount amount deducted from the invoice (`MyInvois Total Discount Value / AllowanceTotalAmount`). If provided, must be a non-negative number. Omit when there is no invoice-level discount. |
| items                 | array  | Yes      | Array of line items (see below). |


### items[] — line item fields

| Field        | Type   | Required | Description |
|--------------|--------|----------|-------------|
| description  | string | Yes      | Line item description. |
| quantity     | number | Yes      | Quantity (must be ≥ 1). |
| amount       | number | Yes      | Line amount before tax (must be ≥ 0). |
| tax_amount   | number | Yes      | Line tax amount (must be ≥ 0). |

### Respond Example

```json
{
    "status_code": 200,
    "request_id": "1234567890.uuid",
    "message": "All 1 invoice submitted successfully.",
    "data": [
        {
            "status": "success",
            "input": { ...
            },
            "remarks": "E-invoice submitted successfully",
            "submission_id": "EP-MEI123456"
        }
    ]
}
```
On validation error, data is an array of error strings and status_code is 400.

<h3 id="Notes-Malaysia-E-invoice-2026-03">Important Notes</h3>

1. UTC timezone required: Both invoice_issue_date and invoice_issue_time must be in UTC timezone.
  - invoice_issue_time is provided as HH:mm:ss; the system appends Z automatically (e.g. "06:30:00" → "06:30:00Z").
  - For Malaysia (UTC+8), convert local time to UTC before submitting (e.g. 2:30 PM MYT = "06:30:00" UTC).
2. Currency: order_currency must be "MYR".
3. Multiple line items: Each bulk invoice supports multiple line items via items[]. Invoice totals are automatically summed from all line items.
4. SST number: sst_no is optional; 

<h3 id="Reference-Malaysia-E-invoice-2026-03">State Codes Reference (Malaysia)</h3>

| Code | State                               |
|------|-------------------------------------|
| 1    | Johor                               |
| 2    | Kedah                               |
| 3    | Kelantan                            |
| 4    | Melaka                              |
| 5    | Negeri Sembilan                     |
| 6    | Pahang                              |
| 7    | Pulau Pinang                        |
| 8    | Perak                               |
| 9    | Perlis                              |
| 10   | Selangor                            |
| 11   | Terengganu                          |
| 12   | Sabah                               |
| 13   | Sarawak                             |
| 14   | Wilayah Persekutuan Kuala Lumpur    |
| 15   | Wilayah Persekutuan Labuan          |
| 16   | Wilayah Persekutuan Putrajaya       |

### Example cURL Request

```json
curl -X POST https: //api.example.com/2026-03/einvoice/malaysia/submit \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "tin_no": "IG12345678901",
    "id_no": "123456789",
    "id_type": "BRN",
    "sst_no": "A12-3456-78901234",
    "company_name": "ABC Sdn. Bhd.",
    "company_phone": "+60123456789",
    "msic_code": "63120",
    "business_nature": "OPERATING A WEB-BASED PARCEL CONSOLIDATOR",
    "address_line_1": "1-10-05, Suntech @ Penang Cybercity",
    "city": "Pulau Pinang",
    "postcode": "11950",
    "state_code": "07",
    "bulk": [
        {
            "invoice_no": "EI-2601-ZZHKB",
            "invoice_issue_date": "2024-01-15",
            "invoice_issue_time": "14:30:00",
            "order_currency": "MYR",
            "items": [
                {
                    "description": "Shipping Services - Order #12345",
                    "quantity": 1,
                    "amount": 100.00,
                    "tax_amount": 6.00
                }
            ]
        },
        {
            "invoice_no": "EI-2601-ZZHKC",
            "invoice_issue_date": "2024-01-15",
            "invoice_issue_time": "15:45:00",
            "order_currency": "MYR",
            "items": [
                {
                    "description": "Express Delivery - Order #12346",
                    "quantity": 1,
                    "amount": 200.00,
                    "tax_amount": 12.00
                },
                {
                    "description": "Insurance - Order #12346",
                    "quantity": 1,
                    "amount": 50.50,
                    "tax_amount": 3.03
                }
            ]
        }
    ]
}'
```





