# Shipment Quotations

Get shipment quotations from all available courier companies on the EasyParcel platform. Provide sender and receiver addresses to receive pricing details, available services, and additional features.

## Authentication (Standard Quotation)

> To authorize, use this code:

```shell
curl "https://api.easyparcel.com/open_api/2025-09/shipment/quotations" \
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

## HTTP Request (Quotation)

`POST https://api.easyparcel.com/open_api/2025-09/shipment/quotations`

## Quotation Request

> Example Request:

```json
{
  "shipment": [
    {
      "sender": {
        "postcode": "10150",
        "subdivison_code": "MY-02",
        "country": "MY"
      },
      "receiver": {
        "postcode": "10150",
        "subdivison_code": "MY-02",
        "country": "MY"
      },
      "parcel_value":50,
      "weight": 0.5,
      "width": 5,
      "length": 5,
      "height": 5
    },
     {
      "sender": {
        "postcode": "10150",
        "subdivison_code": "MY-02",
        "country": "MY"
      },
      "receiver": {
        "postcode": "14000",
        "subdivison_code": "MY-02",
        "country": "MY"
      },
      "weight": 0.5,
      "width": 5,
      "length": 5,
      "height": 5
    },
    {
      "sender": {
        "postcode": "10150",
        "subdivison_code": "MY-02",
        "country": "MY"
      },
      "receiver": {
        "postcode": "09000",
        "subdivison_code": "MY-07",
        "country": "MY"
      },
      "weight": 0.5,
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
subdivison_code | string(35) | true | Sender's subdivision code (ISO 3166)
country | string(2) | true | Sender's country code

### Receiver Parameters

Parameter | Type | Required | Description
--------- | ---- | -------- | -----------
postcode | string(10) | true | Receiver's postcode  
subdivison_code | string(35) | true | Receiver's subdivision code (ISO 3166)
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

## Quotation Response 

> Example Response:

```json
{
    "status_code": 200,
    "message": "1 requests success, 0 request error.",
    "data": [
        {
            "status": "success",
            "input": {
                "sender": {
                    "postcode": "10150",
                    "subdivison_code": "MY-02",
                    "country": "MY"
                },
                "receiver": {
                    "postcode": "018916",
                    "subdivison_code": "SG-04",
                    "country": "SG"
                },
                "parcel_value": 50,
                "weight": 0.5,
                "width": 5,
                "length": 5,
                "height": 5
            },
            "quotations": [
                {
                    "courier": {
                        "service_id": "EP-CS09O",
                        "service_name": "Aramex International- Economy (Pick Up)",
                        "courier_id": "EP-CR0AE",
                        "courier_name": "Aramex International",
                        "courier_logo": "https://s3-ap-southeast-1.amazonaws.com/easyparcel/Public/source/general/img/couriers/Aramex_International.jpg",
                        "delivery_duration": null,
                        "service_tag": [
                            {
                                "name": "Service Label",
                                "value": "Economy"
                            },
                            {
                                "name": "Service Destinations",
                                "value": "International"
                            },
                            {
                                "name": "Service Methods",
                                "value": "Pick Up"
                            }
                        ]
                    },
                    "pricing": {
                        "currency": "MYR",
                        "total_amount": "21.50",
                        "shipment_price": "21.00",
                        "total_features_price": "0.50"
                    },
                    "features": [
                        {
                            "cod": {
                                "available": false,
                                "min_cod_amount": "",
                                "max_cod_amount": "",
                                "charges_description": ""
                            }
                        },
                        {
                            "sms_tracking": {
                                "sms_price": "0.20",
                                "custom_sms_price": "0.05",
                                "remove_ep_branding_price": "0.05"
                            }
                        },
                        {
                            "email_tracking": {
                                "email_price": "0.05",
                                "custom_email_price": "0.05",
                                "remove_ep_branding_price": "0.05"
                            }
                        },
                        {
                            "whatsapp_tracking": {
                                "whatsapp_price": "0.25"
                            }
                        }
                    ]
                }
            ]
        }
    ]
}
```

### Quotation Response

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

### Pricing Information

Parameter | Type | Description
--------- | ---- | -----------
currency | string | Currency code (e.g., MYR, USD)
total_amount | string | Final total including all fees
shipment_price | string | Base shipping price
total_features_price | string | Additional features cost

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

## Code Examples

Select a language from the options on the right to switch between PHP, JavaScript, and Python examples.

```javascript
async function getShippingQuotes(senderPostcode, receiverPostcode) {
  const requestData = {
    list: [{
      sender: {
        postcode: senderPostcode,
        subdivison_code: "MY-02",
        country: "MY"
      },
      receiver: {
        postcode: receiverPostcode,
        subdivison_code: "SG-04", 
        country: "SG"
      },
      weight: 0.5,
      width: 5,
      length: 5,
      height: 5,
      parcel_value: 50
    }]
  };

  try {
    const response = await fetch(
      'https://api.easyparcel.com/open_api/2025-09/shipment/quotations',
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
        'list' => [[
            'sender' => [
                'postcode' => $senderPostcode,
                'subdivison_code' => 'MY-02',
                'country' => 'MY'
            ],
            'receiver' => [
                'postcode' => $receiverPostcode,
                'subdivison_code' => 'SG-04',
                'country' => 'SG'
            ],
            'weight' => 0.5,
            'width' => 5,
            'length' => 5,
            'height' => 5,
            'parcel_value' => 50
        ]]
    ];

    $ch = curl_init('https://api.easyparcel.com/open_api/2025-09/shipment/quotations');
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
        "list": [{
            "sender": {
                "postcode": sender_postcode,
                "subdivison_code": "MY-02",
                "country": "MY"
            },
            "receiver": {
                "postcode": receiver_postcode,
                "subdivison_code": "SG-04",
                "country": "SG"
            },
            "weight": 0.5,
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
            'https://api.easyparcel.com/open_api/2025-09/shipment/quotations',
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

## Error Handling

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
                    "subdivison_code": "MY-02",
                    "country": "MY"
                },
                "receiver": {
                    "country": "SG"
                },
                "weight": 0.5
            },
            "errors": [
                "The receiver postcode field is required"
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

## Best Practices for Shipping Quotation
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
