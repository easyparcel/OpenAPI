# Insurance Quotation Feature

The insurance quotation feature allows customers to retrieve pricing information for shipment insurance coverage. This helps users understand the cost of insuring their valuable parcels and make informed decisions about protecting their shipments against loss or damage.

## Retrieving Insurance Quotations

Customers can retrieve insurance pricing for one or multiple shipments using the following endpoint:

## HTTP Request (Insurance Quotation)

`POST https://api.easyparcel.com/open_api/2025-12/insurance_quotations`

This endpoint returns detailed insurance pricing based on shipment details including courier, origin, destination, weight, and item values.

## Insurance Quotation Request

### Submitting Shipment Details to Get Insurance Pricing

You can submit multiple shipment scenarios in a single request to retrieve insurance quotations for batch processing.

### Sample Insurance Quotation Request:

```json
{
  "list": [
    {
      "courier_id": "EP-CR0AP",
      "currency_code": "MYR",
      "from_postcode": "10150",
      "from_country": "MY",
      "to_postcode": "11950",
      "to_country": "MY",
      "shipment_weight": 1.5,
      "shipment_item": [
        {
          "value": 50,
          "quantity": 3,
          "currency_code": "MYR"
        }
      ]
    },
    {
      "courier_id": "EP-CR0AW",
      "currency_code": "MYR",
      "from_postcode": "10150",
      "from_country": "MY",
      "to_postcode": "11950",
      "to_country": "MY",
      "shipment_weight": 1.5,
      "shipment_item": [
        {
          "value": 50,
          "quantity": 3,
          "currency_code": "MYR"
        }
      ]
    }
  ]
}
```

### Request Parameters

| Parameter | Type  | Required | Description                                    |
|-----------|-------|----------|------------------------------------------------|
| list      | array | Yes      | Array of shipment objects to get insurance quotes for |

### Shipment Object (Inside `list` array)

| Parameter       | Type   | Required | Description                                           |
|-----------------|--------|----------|-------------------------------------------------------|
| courier_id      | string | Yes      | EasyParcel courier service ID (e.g., "EP-CR0AW")     |
| currency_code   | string | Yes      | Currency code for the quotation (e.g., "MYR")        |
| from_postcode   | string | Yes      | Origin postcode                                       |
| from_country    | string | Yes      | Origin country code (ISO 3166-1 alpha-2, e.g., "MY") |
| to_postcode     | string | Yes      | Destination postcode                                  |
| to_country      | string | Yes      | Destination country code (ISO 3166-1 alpha-2)        |
| shipment_weight | number | Yes      | Total shipment weight in kilograms                    |
| shipment_item   | array  | Yes      | Array of item objects to be insured                   |

### Item Object (Inside `shipment_item` array)

| Parameter     | Type   | Required | Description                                    |
|---------------|--------|----------|------------------------------------------------|
| value         | number | Yes      | Declared value of the item                     |
| quantity      | int    | Yes      | Quantity of items                              |
| currency_code | string | Yes      | Currency code for the item value (e.g., "MYR") |


## Insurance Quotation Response

### Insurance Quotation API - Response Parameters

### Sample Response for Insurance Quotations

```json
{
    "status_code": 200,
    "message": "2 requests success, 0 request error.",
    "data": [
        {
            "status": "success",
            "input": {
                "courier_id": "EP-CR0AP",
                "currency_code": "MYR",
                "from_postcode": "10150",
                "from_country": "MY",
                "to_postcode": "11950",
                "to_country": "MY",
                "shipment_weight": 1.5,
                "shipment_item": [
                    {
                        "value": 50,
                        "quantity": 3,
                        "currency_code": "MYR"
                    }
                ]
            },
            "insurance_quotations": [
                {
                    "insurance_service_id": "EP-IR0D",
                    "insurance_service_name": "EasyCover",
                    "insurance_cover_notice": "for lost",
                    "currency_code": "MYR",
                    "charge_amount": 7.5,
                    "pricing": {
                        "currency_code": "MYR",
                        "charge_amount": 7.5,
                        "base_fee": 0,
                        "max_item_value": null,
                        "min_item_value": "200.01",
                        "percentage_rate": "0.025",
                        "max_item_value_coverage": 10000
                    }
                }
            ]
        },
        {
            "status": "success",
            "input": {
                "courier_id": "EP-CR0AW",
                "currency_code": "MYR",
                "from_postcode": "10150",
                "from_country": "MY",
                "to_postcode": "11950",
                "to_country": "MY",
                "shipment_weight": 1.5,
                "shipment_item": [
                    {
                        "value": 50,
                        "quantity": 3,
                        "currency_code": "MYR"
                    }
                ]
            },
            "insurance_quotations": [
                {
                    "insurance_service_id": "EP-IR0D",
                    "insurance_service_name": "EasyCover",
                    "insurance_cover_notice": "for lost",
                    "currency_code": "MYR",
                    "charge_amount": 75,
                    "pricing": {
                        "currency_code": "MYR",
                        "charge_amount": 75,
                        "base_fee": 0,
                        "max_item_value": null,
                        "min_item_value": "200.01",
                        "percentage_rate": "0.025",
                        "max_item_value_coverage": 10000
                    }
                }
            ]
        }
    ]
}
```

### Main Response

| Parameter    | Type   | Description                                                      |
|--------------|--------|------------------------------------------------------------------|
| status_code  | int    | HTTP status code indicating success or failure                   |
| request_id   | string | Unique identifier for the API request                            |
| message      | string | Summary of the response (e.g., number of successful/failed requests) |
| data         | array  | Array of quotation result objects                                |

### Quotation Result Object (Inside `data` array)

| Parameter             | Type   | Description                                                  |
|-----------------------|--------|--------------------------------------------------------------|
| status                | string | Status of the quotation request ("success" or "error")       |
| input                 | object | Echo of the input parameters sent in the request             |
| insurance_quotations  | array  | Array of available insurance options for this shipment       |

### Insurance Quotation Object (Inside `insurance_quotations` array)

| Parameter               | Type   | Description                                              |
|-------------------------|--------|----------------------------------------------------------|
| insurance_service_id    | string | Unique identifier for the insurance service              |
| insurance_service_name  | string | Display name of the insurance service (e.g., "EasyCover") |
| insurance_cover_notice  | string | Coverage details or notice (e.g., "for lost")            |
| currency_code           | string | Currency code for the insurance charge                   |
| charge_amount           | number | Total insurance charge amount                            |
| pricing                 | object | Detailed pricing breakdown for the insurance             |

### Pricing Object (Inside `insurance_quotations`)

| Parameter                | Type   | Description                                                 |
|--------------------------|--------|-------------------------------------------------------------|
| currency_code            | string | Currency code for pricing                                   |
| charge_amount            | number | Calculated insurance charge based on item value             |
| base_fee                 | number | Base fee for insurance (if applicable)                      |
| max_item_value           | number | Maximum item value for this pricing tier (null if no max)  |
| min_item_value           | string | Minimum item value required for this insurance tier         |
| percentage_rate          | string | Percentage rate applied to item value (e.g., "0.025" = 2.5%) |
| max_item_value_coverage  | number | Maximum coverage amount available for items                 |



## Understanding Insurance Pricing

Insurance charges are typically calculated based on:

1. **Base Fee**: A flat fee that applies regardless of item value (if applicable)
2. **Percentage Rate**: A percentage of the declared item value
3. **Value Tiers**: Different rates may apply based on item value ranges

### Example Calculation:

For an item valued at MYR 3,000:
- Base Fee: MYR 0
- Percentage Rate: 2.5% (0.025)
- Calculation: (3,000 × 0.025) + 0 = **MYR 75**

<h2 id="insurance-usage-note">Usage Notes (Insurance Quotation)</h2>

- **Batch Quotations**: You can request insurance quotes for multiple shipments in a single API call for efficiency.
- **Currency Consistency**: Ensure the currency codes match across shipment items and quotation requests.
- **Coverage Limits**: Note the `max_item_value_coverage` to understand the maximum insured amount available.
- **Minimum Values**: Items below the `min_item_value` threshold may not be eligible for insurance or may use different pricing.
- **Multiple Options**: Some shipments may have multiple insurance service options available with different pricing structures.

<h2 id="insurance-example-use-cases">Example Use Cases</h2>

### Single Shipment Quotation

```json
{
  "list": [
    {
      "courier_id": "EP-CR0AP",
      "currency_code": "MYR",
      "from_postcode": "50000",
      "from_country": "MY",
      "to_postcode": "10450",
      "to_country": "MY",
      "shipment_weight": 1.5,
      "shipment_item": [
        {
          "value": 1500,
          "quantity": 1,
          "currency_code": "MYR"
        }
      ]
    }
  ]
}
```

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

### Multiple Items in One Shipment

```json
{
  "list": [
    {
      "courier_id": "EP-CR0AW",
      "currency_code": "MYR",
      "from_postcode": "11900",
      "from_country": "MY",
      "to_postcode": "11900",
      "to_country": "MY",
      "shipment_weight": 3,
      "shipment_item": [
        {
          "value": 500,
          "quantity": 2,
          "currency_code": "MYR"
        },
        {
          "value": 800,
          "quantity": 1,
          "currency_code": "MYR"
        }
      ]
    }
  ]
}
```

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

### International Shipment

```json
{
  "list": [
    {
      "courier_id": "EP-CR0D9",
      "currency_code": "MYR",
      "from_postcode": "11900",
      "from_country": "MY",
      "to_postcode": "10001",
      "to_country": "US",
      "shipment_weight": 2,
      "shipment_item": [
        {
          "value": 5000,
          "quantity": 1,
          "currency_code": "MYR"
        }
      ]
    }
  ]
}
```

## Applying Insurance to Shipments

Once you receive an insurance quotation, you can apply the insurance to your shipment by including the `insurance_service_id` in your shipment submission request.

### Example Insurance Application in Shipment Submission:

```json
{
  "shipment": [
    {
      "service_id": "EP-CS096",
      "insurance_service_id": "EP-IR0D",
      // ... other shipment details
    }
  ]
}
```


<h2 id="insurance-error-handling">Error Handling</h2>

If a quotation request fails, the response will include an error status:

```json
{
    "status_code": 200,
    "message": "0 requests success, 2 request error.",
    "data": [
        {
            "status": "error",
            "input": {
                "courier_id": "EP-CR0AP",
                "currency_code": "MYR",
                "from_postcode": "10150",
                "from_country": "MY",
                "to_postcode": "11950",
                "to_country": "MY",
                "shipment_weight": 1.5,
                "shipment_item": [
                    {
                        "value": 50,
                        "quantity": 3,
                        "currency_code": "MYR"
                    }
                ]
            },
            "errors": [
                "Insurance service not available for this request"
            ]
        },
        {
            "status": "error",
            "input": {
                "courier_id": "",
                "currency_code": "MYR",
                "from_postcode": "10150",
                "from_country": "MY",
                "to_postcode": "11950",
                "to_country": "MY",
                "shipment_weight": 1.5,
                "shipment_item": [
                    {
                        "value": 50,
                        "quantity": 3,
                        "currency_code": "MYR"
                    }
                ]
            },
            "errors": [
                "The courier id field is required "
            ]
        }
    ]
}
```





