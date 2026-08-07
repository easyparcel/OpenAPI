<h1 id="od-shipment-listing-2026-06">OnDemand Shipment Listing</h1>

<h2 id="od-shipment-listing-overview-2026-06">OnDemand Shipment Listing Overview</h2>

This feature allows users to retrieve a paginated list of their on-demand shipments booked through the EasyParcel platform. The listing returns each booking's identifier, order number, tracking URL, current status, price paid, and the courier/transport used. Only the shipments belonging to the requesting account are returned — no account identifier is sent in the request.

Pagination is **cursor based** (not offset based). Every response carries a `pagination` object holding a `next_page_token`; passing that token back in the next request returns the following page. Any filter applied on the first request (`status`, `date_from`, `date_to`) is embedded inside the token, so subsequent pages stay consistent without re-sending the filters.

<h2 id="http-request-od-shipment-listing-2026-06">HTTP Request (OnDemand Shipment Listing)</h2>

`POST https://api.easyparcel.com/open_api/2026-06/ondemand/list`

<h2 id="od-shipment-listing-request-parameters-2026-06">OnDemand Shipment Listing Request Parameters</h2>

### Request Sample

```json
{
  "limit": 50,
  "status": 3,
  "date_from": "2026-06-01",
  "date_to": "2026-06-30"
}
```

### Request Sample (Next Page)

```json
{
  "limit": 50,
  "page_token": "eyJsYXN0X2lkIjo5ODc2NSwiZmlsdGVycyI6eyJzdGF0dXMiOjN9fQ=="
}
```

### Main Structure

| Parameter                 | Type    | Required | Description                                                                     | Remarks                                                                       |
| ------------------------- | ------- | -------- | ------------------------------------------------------------------------------- | ----------------------------------------------------------------------------- |
| limit                     | integer | No       | Number of records per page                                                       | Default `50`. Maximum `250`. Any value below `1` falls back to `50`            |
| page\_token               | string  | No       | Cursor returned as `pagination.next_page_token` in the previous response         | Base64 encoded. When present, `status` / `date_from` / `date_to` are ignored   |
| before\_shipment\_number  | string  | No       | Return only shipments created before this `order_number`                         | Alternative cursor. Ignored when `page_token` is supplied                      |
| status                    | integer | No       | Filter by shipment status code                                                   | See [Status Codes](#status-codes-od-shipment-listing-2026-06)                  |
| date\_from                | string  | No       | Filter shipments created on or after this date (`YYYY-MM-DD`)                     | Expanded internally to `date_from 00:00:00`                                   |
| date\_to                  | string  | No       | Filter shipments created on or before this date (`YYYY-MM-DD`)                    | Expanded internally to `date_to 23:59:59`                                     |

> **Filter behaviour with pagination.** Filters are only read from the request on the **first** page (when no `page_token` is sent). They are then persisted inside the returned token. Sending both a `page_token` and a fresh `status` / `date_from` / `date_to` will silently keep the *token's* filters, not the new ones. To change filters, start a new listing without a `page_token`.

<h2 id="status-codes-od-shipment-listing-2026-06">Status Codes</h2>

| status | status\_text            |
| ------ | ----------------------- |
| 0      | Cancelled by Customer   |
| 1      | Pending                 |
| 2      | Accepted                |
| 3      | In Transit              |
| 4      | Cancelled by Admin      |
| 5      | Cancelled by Driver     |
| 6      | Fulfilled               |
| 7      | Unable to Find Driver   |

<h2 id="response-parameters-od-shipment-listing-2026-06">OnDemand Shipment Listing Response Parameters</h2>

### Sample Response

```json
{
    "status_code": 200,
    "request_id": "1770000000000.a1b2c3d4-e5f6-7890-abcd-ef1234567890",
    "message": "success",
    "data": [
        {
            "booking_id": "EOD-98765",
            "order_number": "3550938272853338459",
            "tracking_url": "https://test.com",
            "status": 3,
            "status_text": "In Transit",
            "payment": {
                "currrency_code": "MYR",
                "price": "7.06"
            },
            "ondemand_service": {
                "partner": {
                    "courier_name": "Lalamove",
                    "courier_image": "https://s3-ap-southeast-1.amazonaws.com/easyparcel-static/Public/source/general/img/couriers/lalamove.svg"
                },
                "transportation": {
                    "transportation": "Bike"
                }
            }
        },
        {
            "booking_id": "EOD-98760",
            "order_number": "3554238272853338459",
            "tracking_url": "https://test2.com",
            "status": 6,
            "status_text": "Fulfilled",
            "payment": {
                "currrency_code": "MYR",
                "price": "27.06"
            },
            "ondemand_service": {
                "partner": {
                    "courier_name": "PandaGo",
                    "courier_image": "https://s3-ap-southeast-1.amazonaws.com/easyparcel-static/Public/source/general/img/couriers/pandaGo_pink.png"
                },
                "transportation": {
                    "transportation": "Car"
                }
            }
        }
    ],
    "pagination": {
        "next_page_token": "eyJsYXN0X2lkIjo5ODc2MCwiZmlsdGVycyI6eyJzdGF0dXMiOjN9fQ==",
        "next_shipment_number": "3548576315576234844",
        "has_more": true,
        "limit": 50,
        "filter_applied": {
            "status": 3,
            "status_code": 3
        }
    }
}
```

### Main Structure

| Parameter    | Type   | Description                                          |
| ------------ | ------ | ---------------------------------------------------- |
| status\_code | int    | HTTP status code                                     |
| request\_id  | string | Unique request identifier                            |
| message      | string | Status message                                       |
| data         | array  | List of on-demand shipments                          |
| pagination   | object | Cursor pagination metadata                           |

### Data Object Structure

| Section           | Parameter                     | Type   | Description                                                              |
| ----------------- | ----------------------------- | ------ | ------------------------------------------------------------------------ |
| —                 | booking\_id                   | string | EasyParcel booking ID, prefixed `EOD-` (e.g. `EOD-98765`)                |
| —                 | order\_number                 | string | On-demand order number                                                   |
| —                 | tracking\_url                 | string | Public tracking URL for the shipment                                     |
| —                 | status                        | int    | Status code — see [Status Codes](#status-codes-od-shipment-listing-2026-06) |
| —                 | status\_text                  | string | Human readable status                                                    |
| payment           | currrency\_code               | string | Currency of the amount charged (e.g. `MYR`) — **note the spelling of this key** |
|                   | price                         | string | Amount charged for the shipment                                          |
| ondemand\_service | partner.courier\_name         | string | Courier short name                                                       |
|                   | partner.courier\_image        | string | Courier logo URL                                                         |
|                   | transportation.transportation | string | Transport type (e.g. `Bike`, `Car`, `Van`)                               |

> **Known field spelling.** The payment currency key is returned as `currrency_code` (three `r`s). It is kept as-is for backward compatibility — parse it exactly as spelled.

### Pagination Object Structure

| Parameter               | Type            | Description                                                                                         |
| ----------------------- | --------------- | --------------------------------------------------------------------------------------------------- |
| next\_page\_token       | string \| null  | Cursor for the next page. `null` when there are no further pages                                     |
| next\_shipment\_number  | string \| null  | `order_number` of the last record on this page — usable as `before_shipment_number`. `null` on the last page |
| has\_more               | boolean         | `true` when more records exist beyond this page                                                      |
| limit                   | int             | Effective page size applied to this request                                                          |
| filter\_applied         | object \| null  | Filters currently in effect. `null` when no filter was applied                                       |

---

<h2 id="sample-error-response-od-shipment-listing-2026-06">Sample Error Response</h2>

### 401 – Unauthorized

Returned when the access token does not resolve to an account.

```json
{
    "status_code": 401,
    "request_id": "1770000000000.a1b2c3d4-e5f6-7890-abcd-ef1234567890",
    "message": "Unauthorized Access",
    "data": "Invalid Access Token"
}
```

### 400 – Invalid Page Token

Returned when `page_token` is not a valid base64 encoded cursor produced by this endpoint.

```json
{
    "status_code": 400,
    "request_id": "1770000000000.a1b2c3d4-e5f6-7890-abcd-ef1234567890",
    "message": "Invalid page token",
    "data": []
}
```

<h2 id="code-implementation-od-shipment-listing-2026-06">OnDemand Shipment Listing Code Implementation Examples</h2>

### JavaScript (Fetch API) | PHP (cURL) | Python (requests)

```javascript
async function listOndemandShipments(token, pageToken = null) {
  const requestData = pageToken
    ? { limit: 50, page_token: pageToken }
    : { limit: 50, status: 3, date_from: "2026-06-01", date_to: "2026-06-30" };

  const res = await fetch('https://api.easyparcel.com/open_api/2026-06/ondemand/list', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
      'Authorization': `Bearer ${token}`
    },
    body: JSON.stringify(requestData)
  });
  return res.json();
}

// Walk every page
(async () => {
  let pageToken = null;
  do {
    const page = await listOndemandShipments('YOUR_ACCESS_TOKEN', pageToken);
    page.data.forEach(s => console.log(s.booking_id, s.status_text));
    pageToken = page.pagination.next_page_token;
  } while (pageToken);
})();
```

```php
<?php
function list_ondemand_shipments($token, $pageToken = null) {
    $data = $pageToken
        ? ["limit" => 50, "page_token" => $pageToken]
        : ["limit" => 50, "status" => 3, "date_from" => "2026-06-01", "date_to" => "2026-06-30"];

    $ch = curl_init('https://api.easyparcel.com/open_api/2026-06/ondemand/list');
    curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
    curl_setopt($ch, CURLOPT_POST, true);
    curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode($data));
    curl_setopt($ch, CURLOPT_HTTPHEADER, [
        'Content-Type: application/json',
        'Authorization: Bearer ' . $token
    ]);
    $response = curl_exec($ch);
    curl_close($ch);
    return json_decode($response, true);
}

$pageToken = null;
do {
    $page = list_ondemand_shipments('YOUR_ACCESS_TOKEN', $pageToken);
    foreach ($page['data'] as $shipment) {
        echo $shipment['booking_id'] . ' - ' . $shipment['status_text'] . PHP_EOL;
    }
    $pageToken = $page['pagination']['next_page_token'];
} while ($pageToken);
?>
```

```python
import requests

url = 'https://api.easyparcel.com/open_api/2026-06/ondemand/list'
headers = {
    'Content-Type': 'application/json',
    'Authorization': 'Bearer YOUR_ACCESS_TOKEN'
}

page_token = None
while True:
    data = {"limit": 50, "page_token": page_token} if page_token else {
        "limit": 50,
        "status": 3,
        "date_from": "2026-06-01",
        "date_to": "2026-06-30"
    }

    page = requests.post(url, json=data, headers=headers).json()
    for shipment in page['data']:
        print(shipment['booking_id'], shipment['status_text'])

    page_token = page['pagination']['next_page_token']
    if not page_token:
        break
```

<h2 id="best-practices-od-shipment-listing-2026-06">Best Practices for OnDemand Shipment Listing</h2>

1. **Always paginate with the token** – Use `pagination.next_page_token` verbatim instead of building your own cursor; the token also carries the filter state.
2. **Set filters on the first call only** – Once a `page_token` exists, filters are locked in. Restart the listing without a token to change them.
3. **Stop on `has_more: false`** – Do not keep polling after `next_page_token` is `null`; it will simply replay the first page.
4. **Keep `limit` reasonable** – The maximum is `250`, but smaller pages (50–100) give faster responses and steadier latency.
5. **Treat `booking_id` as the handle** – Pass it straight to `POST /2026-06/ondemand/details` to fetch the full order, including waypoints and driver details.
6. **Guard the currency key spelling** – The payment currency is `currrency_code`, not `currency_code`. Take note that this typo will be fixed in next version.
7. **Store status codes, display status text** – Filter on the numeric `status`; show `status_text` to end users.
