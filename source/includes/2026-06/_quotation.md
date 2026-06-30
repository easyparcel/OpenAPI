<h1 id="shipment-quotation-2026-06">Shipment Quotations</h1>

Get shipment quotations from all available courier companies on the EasyParcel platform. Provide sender and receiver addresses to receive pricing details, available services, and additional features.

<h2 id="quotation-authentication-2026-06">Authentication (Standard Quotation)</h2>

> To authorize, use this code:

```shell
curl "https://api.easyparcel.com/open_api/2026-06/shipment/quotations" \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN"
```

```javascript
const headers = {
  'Authorization': 'Bearer YOUR_ACCESS_TOKEN',
  'Content-Type': 'application/json'
};
```

```php
$headers = [
    'Authorization: Bearer YOUR_ACCESS_TOKEN',
    'Content-Type: application/json'
];
```

```python
headers = {
    'Authorization': 'Bearer YOUR_ACCESS_TOKEN',
    'Content-Type': 'application/json'
}
```

EasyParcel uses Oauth 2.0  to allow access to the API. You can register a new Oauth 2.0 access at our [developer portal](https://developer.easyparcel.com).

The API expects the Oauth 2.0 to be included in all API requests to the server in a header that looks like the following:

`Authorization: Bearer YOUR_ACCESS_TOKEN`

<h2 id="http-request-quotation-2026-06">HTTP Request (Quotation)</h2>

`POST https://api.easyparcel.com/open_api/2026-06/shipment/quotations`

<h2 id="quotation-request-2026-06">Quotation Request</h2>

> Example Request:

```json
{
  "shipment": [
    {
      "sender": {
        "postcode": "10150",
        "subdivision_code": "MY-07",
        "country": "MY"
      },
      "receiver": {
        "postcode": "11950",
        "subdivision_code": "MY-07",
        "country": "MY"
      },
      "parcel_value":50,
      "weight": 1.5,
      "width": 5,
      "length": 5,
      "height": 5
    }
    
  ]
}
```

### Sender Parameters

Parameter | Type | Required | Description
--------- | ---- | -------- | -----------
postcode | string(10) | true | Sender's postcode
subdivision_code | string(35) | true | Sender's subdivision code (ISO 3166)
country | string(2) | true | Sender's country code

### Receiver Parameters

Parameter | Type | Required | Description
--------- | ---- | -------- | -----------
postcode | string(10) | true | Receiver's postcode  
subdivision_code | string(35) | true | Receiver's subdivision code (ISO 3166)
country | string(2) | true | Receiver's country code

### Parcel Parameters

Parameter | Type | Required | Description
--------- | ---- | -------- | -----------
weight | double(8,2) | true | Parcel weight in KG
width | double(8,2) | false | Parcel width in CM
height | double(8,2) | false | Parcel height in CM
length | double(8,2) | false | Parcel length in CM
parcel_value | double(8,2) | false | Parcel value in account currency

<aside class="notice">
The request uses nested objects for sender and receiver information.
</aside>

### BYOC Request Option

<details>
<summary>What is <strong>BYOC (Bring Your Own Courier)</strong>?</summary>
<p>BYOC (Bring Your Own Courier) lets an account use its own linked courier accounts (for example FedEx or GDEX) through EasyParcel. When an account has linked a courier, rates from that courier are returned automatically within the same <code>quotations</code> array, using the same structure as the other rates — no request change is required, and accounts without a linked courier are unaffected.</p>
<p>With BYOC, the courier shipping cost is billed directly to the account's own courier account; EasyParcel charges only a platform fee plus tax (<code>byoc_charges</code> + <code>byoc_charges_tax</code>). Tracking add-ons (SMS, email, WhatsApp) are available for these rates. Linking a courier is done on the EasyParcel portal.</p>
</details>

Parameter | Type | Required | Description
--------- | ---- | -------- | -----------
byoc_no_timeout | boolean | false | Top-level request flag (sibling of `shipment`). By default the live BYOC rate lookup is bounded to 5 seconds so it can never delay the normal rates; if it does not respond within 5 seconds, BYOC rates are simply omitted. Set to `true` to wait for the full BYOC courier response (no 5-second limit) — recommended only when every BYOC rate is required and a slower response is acceptable.

<h2 id="quotation-response-2026-06">Quotation Response </h2>

> Example Response:

```json
{
    "status_code": 200,
    "request_id": "1770285829860.591d8c4f-ca8d-4e8b-9871-28e86ae541d9",
    "message": "1 request success, 0 request error.",
    "data": [
        {
            "status": "success",
            "input": {
                "sender": {
                    "postcode": "10150",
                    "subdivision_code": "MY-07",
                    "country": "MY"
                },
                "receiver": {
                    "postcode": "11950",
                    "subdivision_code": "MY-07",
                    "country": "MY"
                },
                "parcel_value": 50,
                "weight": 1.5,
                "width": 5,
                "length": 5,
                "height": 5
            },
            "quotations": [
                {
                    "courier": {
                        "service_id": "EP-CS096",
                        "service_name": "Aramex (Pick Up)",
                        "courier_id": "EP-CR0AP",
                        "courier_name": "Aramex",
                        "courier_logo": "https://s3-ap-southeast-1.amazonaws.com/easyparcel-static/Public/source/general/img/couriers/Aramex.jpg",
                        "delivery_duration": null,
                        "service_tag": [
                            {
                                "name": "Service Destinations",
                                "value": "Domestic"
                            },
                            {
                                "name": "Service Methods",
                                "value": "Pick Up from Door"
                            },
                            {
                                "name": "Service Methods",
                                "value": "Deliver to Door"
                            },
                            {
                                "name": "Tracking Quality",
                                "value": "Regular"
                            },
                            {
                                "name": "Supported AWB",
                                "value": "Supported AWB size: A6"
                            }
                        ],
                        "is_pickup": true,
                        "is_dropoff": false
                    },
                    "pricing": {
                        "currency": "MYR",
                        "total_amount": "10.84",
                        "shipment_price": "9.80",
                        "shipment_tax": "0.59",
                        "total_features_price": "0.45",
                        "total_features_tax": "0.00"
                    },
                    "features": [
                        {
                            "cod": {
                                "available": true,
                                "min_cod_amount": "MYR10.00",
                                "max_cod_amount": "MYR1000.00",
                                "min_cod_charges": "MYR10.00",
                                "cod_charging_rate": "4.00%",
                                "charges_description": "4.00% of the parcel value or MYR10.00, whichever is higher"
                            }
                        },
                        {
                            "sms_tracking": {
                                "sms_price": "0.20",
                                "custom_sms_price": "0.05",
                                "remove_ep_branding_price": "0.05",
                                "sms_tax": "0.00",
                                "custom_sms_tax": "0.00",
                                "remove_ep_branding_tax": "0.00"
                            }
                        },
                        {
                            "email_tracking": {
                                "email_price": "0.05",
                                "custom_email_price": "0.05",
                                "remove_ep_branding_price": "0.05",
                                "email_tax": "0.00",
                                "custom_email_tax": "0.00",
                                "remove_ep_branding_tax": "0.00"
                            }
                        },
                        {
                            "whatsapp_tracking": {
                                "whatsapp_price": "0.20",
                                "whatsapp_tax": "0.00"
                            }
                        }
                    ]
                }
            ]
        }
    ]
}
```

<h3 id="2-quotation-response-2026-06">Quotation Response</h3>

Parameter | Type | Description
--------- | ---- | -----------
status_code | integer | HTTP status code
message | string | Response message summary
data | array | Array containing quotation results

### Data Object

Parameter | Type | Description
--------- | ---- | -----------
status | string | Request status (success/error)
input | object | Echo of input parameters
quotations | array | Available courier quotations

### Quotation Object

Each quotation contains detailed information about available shipping options:

### Courier Information

Parameter | Type | Description
--------- | ---- | -----------
service_id | string | Unique service identifier
service_name | string | Human-readable service name
courier_id | string | Unique courier identifier  
courier_name | string | Courier company name
courier_logo | string | URL to courier logo image
delivery_duration | string/null | Expected delivery time
service_tag | array | Service categorization tags
is_pickup | boolean | True if pickup service is provided
is_dropoff | boolean | True if dropoff service is provided

### Pricing Information

Parameter | Type | Description
--------- | ---- | -----------
currency | string | Currency code (e.g., MYR, USD)
total_amount | string | Final total including all fees. For a BYOC rate this is the sum of every pricing component: the courier's own shipping cost (`shipment_price`), the EasyParcel BYOC platform charge (`byoc_charges`) and its tax (`byoc_charges_tax`), and the add-ons with their tax (`total_features_price` + `total_features_tax`).
shipment_price | string | Base shipping price. For a BYOC rate this is the courier's own shipping cost, which is billed directly to the account's own courier account (not to EasyParcel).
shipment_tax | string | Tax on the shipment price.
total_features_price | string | Additional features cost
total_features_tax | string | Tax on the additional features
seller_payable_amount | string | The portion of `total_amount` that is actually payable to EasyParcel. For a normal courier this equals the full price (`total_amount`). For a BYOC courier it is the BYOC platform charge plus its tax (`byoc_charges` + `byoc_charges_tax`); the courier's own shipping cost (`shipment_price`) is excluded because it is billed directly to the account's own courier account.
byoc_charges | string | BYOC rates only. EasyParcel's BYOC platform charge for this shipment.
byoc_charges_tax | string | BYOC rates only. Tax on the BYOC platform charge.

### Service Tags

Service tags provide categorization for different shipping services:

Tag Name | Possible Values | Description
-------- | -------------- | -----------
Service Label | Standard, Economy, Priority, EXD | Service speed/tier
Service Destinations | International, Domestic | Geographic scope
Service Methods | Pick Up, Drop-Off | Collection method

<aside class="success">
Use service tags to filter and categorize options in your user interface for better user experience.
</aside>

### Available Features

The API returns various optional features that can be added to shipments:

**Cash on Delivery (COD)**

- `available`: Whether COD is supported
- `min_cod_amount`/`max_cod_amount`: COD limits
- `charges_description`: Additional fee information

**Tracking Services**

- `sms_tracking`: SMS notification pricing
- `email_tracking`: Email notification pricing  
- `whatsapp_tracking`: WhatsApp notification pricing

**Branding Options**

- `awb_branding`: Custom branding on shipping labels
- Includes banner and text customization pricing

**International Shipping**

- `ddp_charges`: Delivered Duty Paid charges
- Includes import taxes, duties, and handling fees

<h2 id="quotation-code-examples-2026-06">Code Examples</h2>

Select a language from the options on the right to switch between cURL, PHP, JavaScript, and Python examples.

```shell
curl -X POST "https://api.easyparcel.com/open_api/2026-06/shipment/quotations" \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "shipment": [
      {
        "sender": { "postcode": "10150", "subdivision_code": "MY-07", "country": "MY" },
        "receiver": { "postcode": "11950", "subdivision_code": "MY-07", "country": "MY" },
        "weight": 1.5,
        "width": 5,
        "length": 5,
        "height": 5,
        "parcel_value": 50
      }
    ]
  }'
```

```javascript
async function getShippingQuotes(senderPostcode, receiverPostcode) {
  const requestData = {
    shipment: [{
      sender: {
        postcode: senderPostcode,
        subdivision_code: "MY-07",
        country: "MY"
      },
      receiver: {
        postcode: receiverPostcode,
        subdivision_code: "MY-07", 
        country: "MY"
      },
      weight: 1.5,
      width: 5,
      length: 5,
      height: 5,
      parcel_value: 50
    }]
  };

  try {
    const response = await fetch(
      'https://api.easyparcel.com/open_api/2026-06/shipment/quotations',
      {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
          'Authorization': 'Bearer YOUR_ACCESS_TOKEN'
        },
        body: JSON.stringify(requestData)
      }
    );

    const data = await response.json();
    
    if (data.status_code === 200) {
      const quotations = data.data[0].quotations;
      // Sort by price (lowest first)
      quotations.sort((a, b) => 
        parseFloat(a.pricing.total_amount) - parseFloat(b.pricing.total_amount)
      );
      return quotations;
    } else {
      throw new Error(data.message);
    }
  } catch (error) {
    console.error('Failed to fetch quotations:', error);
    throw error;
  }
}
```

```php
<?php
function getShippingQuotes($senderPostcode, $receiverPostcode) {
    $requestData = [
        'shipment' => [[
            'sender' => [
                'postcode' => $senderPostcode,
                'subdivision_code' => 'MY-07',
                'country' => 'MY'
            ],
            'receiver' => [
                'postcode' => $receiverPostcode,
                'subdivision_code' => 'MY-07',
                'country' => 'MY'
            ],
            'weight' => 1.5,
            'width' => 5,
            'length' => 5,
            'height' => 5,
            'parcel_value' => 50
        ]]
    ];

    $ch = curl_init('https://api.easyparcel.com/open_api/2026-06/shipment/quotations');
    curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
    curl_setopt($ch, CURLOPT_POST, true);
    curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode($requestData));
    curl_setopt($ch, CURLOPT_HTTPHEADER, [
        'Content-Type: application/json',
        'Authorization: Bearer YOUR_ACCESS_TOKEN'
    ]);

    $response = curl_exec($ch);
    
    if (curl_errno($ch)) {
        throw new Exception('cURL error: ' . curl_error($ch));
    }
    
    curl_close($ch);
    
    $data = json_decode($response, true);
    
    if ($data['status_code'] === 200) {
        $quotations = $data['data'][0]['quotations'];
        
        // Sort by price (lowest first)
        usort($quotations, function($a, $b) {
            return floatval($a['pricing']['total_amount']) - 
                   floatval($b['pricing']['total_amount']);
        });
        
        return $quotations;
    } else {
        throw new Exception($data['message']);
    }
}
?>
```

```python
import requests
import json

def get_shipping_quotes(sender_postcode, receiver_postcode):
    """Get shipping quotations for a parcel."""
    
    request_data = {
        "shipment": [{
            "sender": {
                "postcode": sender_postcode,
                "subdivision_code": "MY-07",
                "country": "MY"
            },
            "receiver": {
                "postcode": receiver_postcode,
                "subdivision_code": "MY-07",
                "country": "MY"
            },
            "weight": 1.5,
            "width": 5,
            "length": 5,
            "height": 5,
            "parcel_value": 50
        }]
    }
    
    headers = {
        'Content-Type': 'application/json',
        'Authorization': 'Bearer YOUR_ACCESS_TOKEN'
    }
    
    try:
        response = requests.post(
            'https://api.easyparcel.com/open_api/2026-06/shipment/quotations',
            headers=headers,
            data=json.dumps(request_data)
        )
        
        data = response.json()
        
        if data['status_code'] == 200:
            quotations = data['data'][0]['quotations']
            
            # Sort by price (lowest first)
            quotations.sort(key=lambda x: float(x['pricing']['total_amount']))
            
            return quotations
        else:
            raise Exception(data['message'])
            
    except requests.exceptions.RequestException as e:
        raise Exception(f"API request failed: {str(e)}")
```

<h2 id="quotation-error-handling-2026-06">Error Handling</h2>

> Error Response Example:

```json
{
    "status_code": 200,
    "message": "0 requests success, 1 request error.",
    "data": [
        {
            "status": "error",
            "input": {
                "sender": {
                    "postcode": "10150",
                    "subdivision_code": "MY-07",
                    "country": "MY"
                },
                "receiver": {
                    "postcode": "",
                    "subdivision_code": "MY-07",
                    "country": "MY"
                },
                "parcel_value": 50,
                "weight": 1.5,
                "width": 5,
                "length": 5,
                "height": 5
            },
            "errors": [
                "The receiver postcode field is required "
            ]
        }
    ]
}
```

The API uses conventional HTTP response codes to indicate success or failure. In addition, the response body contains detailed error information.

### HTTP Status Codes

Code | Meaning
---- | -------
200 | OK -- Request successful (check individual data status)
400 | Bad Request -- Invalid parameters
401 | Unauthorized -- Invalid Oauth 2.0 access token
404 | Not Found -- Endpoint not found
429 | Too Many Requests -- Rate limit exceeded
500 | Internal Server Error -- Server error

### Error Response Structure

Parameter | Type | Description
--------- | ---- | -----------
status | string | Always "error" for failed requests
input | object | The input that caused the error
errors | array | List of specific error messages

<aside class="warning">
Even with HTTP 200 status, individual requests in the batch may fail. Always check the <code>status</code> field in each data object.
</aside>

<h2 id="shipping-quotation-best-practices-">Best Practices for Shipping Quotation</h2>

### Input Validation

Always validate input parameters before making API requests:

- Verify postcode formats for different countries
- Ensure weight and dimensions are positive numbers  
- Check country and subdivision codes against ISO standards

### Rate Limiting

The API implements rate limiting to ensure fair usage:

- Batch multiple shipment quotes in a single request when possible
- Implement exponential backoff for 429 responses
- Cache responses when appropriate to reduce API calls

### User Experience

To provide the best user experience:

- Sort quotations by price (ascending) by default
- Display courier logos and service names clearly
- Show delivery duration when available
- Allow users to toggle optional features
- Highlight popular or recommended services

<aside class="notice">
Consider implementing client-side sorting and filtering to reduce server load and improve response times.
</aside>
