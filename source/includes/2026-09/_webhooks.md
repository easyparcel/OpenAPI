<h1 id="webhook-2026-09"><span style="color: black;"> Webhooks</span></h1>
<h2 id="how-to-subscribe-webhook-2026-09">How to Subscribe to Webhooks</h2>

### Prerequisites

Before setting up webhooks, ensure you have:
- An active EasyParcel developer account
- A configured app in the Developer Hub
- A valid endpoint URL that can receive POST requests
- Your endpoint configured to handle webhook payloads

<h2 id="subscription-steps-2026-09">Subscription Steps</h2>

Follow these steps to subscribe to webhooks:

### 1. 🎯 Navigate to App Settings
- Go to **Developer Hub Dashboard**
- Click on **Apps**
- Select **Settings** on the app you wish to configure webhooks for
<p align="center">
  <img src="https://github.com/user-attachments/assets/922ca5f6-4589-4d0f-88ac-c5da550a132e"
       width="80%" 
       style="border: 1px solid #ddd; border-radius: 8px;">
</p>

### 2. 📡 Access Webhook Configuration
- In the left sidebar, click **Webhook**
- Click the **Add Endpoint** button
<p align="center">
  <img src="https://github.com/user-attachments/assets/a0134580-5361-4f86-863d-4137751e7e14" 
       width="80%" 
       style="border: 1px solid #ccc; border-radius: 8px;">
</p>

### 3. ⚙️ Configure Webhook Details
- **Enter Endpoint URL**: Input the URL that will receive the webhook payload
- **Select Webhook Topic**: Choose the event(s) you want to subscribe to from the available options
- **Verify Configuration**: Double-check your URL and selected topics
<p align="center">
  <img src="https://github.com/user-attachments/assets/cf0b0576-96f1-4474-8d06-d8f74d998086"
       width="70%"
       style="border: 1px solid #ccc; border-radius: 8px;">
</p>


### 4. 💾 Save Configuration
- Press **Save** to confirm your webhook settings
- Your webhook endpoint will be validated

### 5. ✅ Confirmation
- **Done!** Your webhook is now active and will be triggered according to your selected topics
- Test your endpoint to ensure it's receiving webhook data correctly


<h2 id="webhook-topics-2026-09">Webhook Topics</h2>

Every payload carries a `topic` field with the code below, so one endpoint can receive several topics and tell them apart.

| Topic ID | Webhook Topic Name | `topic` value in the payload | Description |
|----------|-------------------|------------------------------|-------------|
| 1 | Shipment Status Update | `shipment.status.update` | Triggered when a shipment status changes |
| 2 | Shipment AWB Update | `shipment.awb.update` | Triggered when a shipment AWB (Air Waybill) is generated or updated |
| 3 | Tracking Status Update | `shipment.tracking.update` | Triggered when package tracking status is updated |
| 4 | Shipment Created | `shipment.create` | Triggered when a new shipment is created |
| 5 | Ondemand Order Status Update | `ondemand.status.update` | Triggered when an on-demand order status changes |

<h2 id="webhook-sample-payload-2026-09">Webhook Sample Payloads</h2>

### Shipment Status Update

```json
{
    "topic": "shipment.status.update",
    "shipment_number": "ES-2504-G7FDF",
    "awb_number": "238725129086",
    "shipment_status_code": 0,
    "shipment_status": "Cancelled",
    "event_date": "2025-04-28 11:40:00"
}
```

| Field | Type | Description |
|-------|------|-------------|
| topic | string | `shipment.status.update` |
| shipment_number | string | EasyParcel shipment number |
| awb_number | string | AWB number. `null` if the shipment has no AWB yet |
| shipment_status_code | int | New status. See [Shipment Status Codes](#webhook-status-codes-2026-09) |
| shipment_status | string | Name of the new status |
| event_date | string | When the status changed (`YYYY-MM-DD HH:MM:SS`, Malaysia time, UTC+8) |

### Shipment AWB Update

```json
{
    "topic": "shipment.awb.update",
    "shipment_number": "ES-2504-G7FDF",
    "awb_number": "23872512999",
    "awb_url": "https://example.com/awb/ES-2504-G7FDF.pdf",
    "awb_url_a4": "https://example.com/awb/ES-2504-G7FDF-a4.pdf",
    "awb_url_a5": null,
    "awb_url_a6": "https://example.com/awb/ES-2504-G7FDF-a6.pdf",
    "tracking_url": "https://easyparcel.com/my/en/track/details/?courier=Skynet&awb=23872512999"
}
```

| Field | Type | Description |
|-------|------|-------------|
| topic | string | `shipment.awb.update` |
| shipment_number | string | EasyParcel shipment number |
| awb_number | string | AWB number |
| awb_url | string | AWB label in your account's preferred label size |
| awb_url_a4 / awb_url_a5 / awb_url_a6 | string | AWB label in each size. `null` when the courier doesn't provide that size |
| tracking_url | string | Public tracking page for the shipment |

### Tracking Status Update

```json
{
    "topic": "shipment.tracking.update",
    "shipment_number": "ES-2504-G7FDF",
    "awb_number": "238725129086",
    "latest_shipment_status_code": 5,
    "latest_tracking_status": "Delivered to recipient",
    "event_date": "2025-04-28 11:40:00",
    "status_log": {
        "0": {
            "event_date": "2025-04-28 11:40:00",
            "shipment_status_code": 5,
            "tracking_status": "Delivered to recipient"
        },
        "1": {
            "event_date": "2025-04-26 12:00:00",
            "shipment_status_code": 3,
            "tracking_status": "Parcel has been collected at Penang"
        }
    },
    "order_info": {
        "order_id": 123456,
        "order_number": "EI-2504-SKMTH",
        "account_id": 1000001
    }
}
```

| Field | Type | Description |
|-------|------|-------------|
| topic | string | `shipment.tracking.update` |
| shipment_number | string | EasyParcel shipment number |
| awb_number | string | AWB number |
| latest_shipment_status_code | int | Status code of the latest event. See [Shipment Status Codes](#webhook-status-codes-2026-09) |
| latest_tracking_status | string | The courier's text for the latest event |
| event_date | string | Time of the latest event, as reported by the courier |
| status_log | object | Every tracking event so far, keyed `"0"`, `"1"`, … newest first, so `"0"` is the latest event. Each has `event_date`, `shipment_status_code` and `tracking_status` |
| order_info | object | The order the shipment belongs to: `order_id`, `order_number`, `account_id` |

### Shipment Created

```json
{
    "topic": "shipment.create",
    "order_number": "EI-2504-SKMTH",
    "shipment_number": "ES-2504-G7FDF",
    "customer_reference_no": "order 1190",
    "price": "8.50",
    "currency_code": "MYR",
    "event_date": "2025-04-28 03:40:00"
}
```

One webhook is sent for each shipment in the order.

| Field | Type | Description |
|-------|------|-------------|
| topic | string | `shipment.create` |
| order_number | string | EasyParcel order number |
| shipment_number | string | EasyParcel shipment number |
| customer_reference_no | string | Your reference for the shipment (`customer_reference_no`, or `reference` if that was not sent) |
| price | string | Shipment price at booking |
| currency_code | string | Currency of `price` |
| event_date | string | When the shipment was created (`YYYY-MM-DD HH:MM:SS`, UTC) |

### Ondemand Order Status Update

```json
{
    "topic": "ondemand.status.update",
    "order_number": "EOD-2506-ABCDE",
    "tracking_url": "https://easyparcel.com/my/en/track/details/?awb=EOD-2506-ABCDE",
    "status": 2,
    "timeline": {
        "create": "2025-06-06 04:20:11",
        "allocate": "2025-06-06 04:21:07"
    },
    "driver": {
        "id": "81994",
        "name": "Test Driver",
        "phone": "+60123456789",
        "photo": "",
        "rating": "",
        "vehicle": { "model": "", "licensePlate": "ABC1234", "physicalVehicleType": "Bike" },
        "coordinates": { "latitude": 5.325513957, "longitude": 100.2862732 }
    },
    "event_date": "2025-06-06 04:21:07",
    "waypoint": [
        { "pod": null, "coordinate": { "latitude": 5.325513957, "longitude": 100.2862732 } },
        { "pod": null, "coordinate": { "latitude": 5.335513957, "longitude": 100.2962732 } }
    ]
}
```

| Field | Type | Description |
|-------|------|-------------|
| topic | string | `ondemand.status.update` |
| order_number | string | EasyParcel on-demand order number |
| tracking_url | string | Tracking page for the order |
| status | int | New status. See [Ondemand Status Codes](#ondemand-status-codes-2026-09) |
| timeline | object | Times of the order's milestones as reported by the provider. Can be `null` |
| driver | object | Driver details once a driver is assigned. Can be `null` |
| event_date | string | When the status changed (`YYYY-MM-DD HH:MM:SS`, UTC) |
| waypoint | array | Each stop's `coordinate`, and `pod` (proof-of-delivery image URL) once available |

<h2 id="webhook-status-codes-2026-09">Shipment Status Codes</h2>

Below are common shipment status codes you may encounter:

| Status Code | Description                    |
|-------------|--------------------------------|
| 0          | Cancel                                |
| 2          | To Be Collected                        |
| 3          | Collected / Parcel been collected at ABC |
| 4          | Delivery In Transit                    |
| 5          | Delivered / Parcel collected by recipient |
| 6          | Returned                               |
| 7          | Schedule In Arrangement                |
| 8          | On Hold                                |
| 11         | Drop Off                               |

<h2 id="ondemand-status-codes-2026-09">Ondemand Status Codes</h2>

Below are the status codes you may encounter in the `ondemand.status.update` webhook:

| Status Code | Description                    |
|-------------|--------------------------------|
| 0           | Cancelled by Customer          |
| 1           | Pending                        |
| 2           | Accepted / Driver On The Way   |
| 3           | In Transit                     |
| 4           | Cancelled by Admin             |
| 5           | Cancelled by Driver            |
| 6           | Fulfilled                      |
| 7           | Unable to Find Driver          |

*Note: Status codes may vary by courier and region. Refer to the API response for the most accurate status description.*

<h2 id="webhook-delivery-retries-2026-09">Delivery and Retries</h2>

- **Timeout**: EasyParcel waits **3 seconds** for your endpoint to respond. Reply quickly, and do any slow work after you have responded.
- **Success**: only an HTTP **200** response counts as delivered. Any other status code (including `201`, `202` and `204`), a timeout or a connection error counts as a failure.
- **Retries**: a failed delivery is retried up to **3 times**, about 5, 10 and 20 minutes after the first attempt. After that the event is not sent again automatically.
- **Duplicates and order**: the same event can arrive more than once, and events can arrive out of order. Use the `Easyparcel-Webhook-Id` header to ignore an event you have already processed, and compare `event_date` for the same `shipment_number` / `order_number` to ignore older updates.

<h2 id="webhook-signature-2026-09">Verifying Webhook Signatures</h2>

Every webhook is signed with your app's **Client Secret** (shown in Developer Hub → Apps → Settings), so you can check that it was sent by EasyParcel and that the body was not changed on the way. Each request carries these headers:

| Header | Description |
|--------|-------------|
| `Easyparcel-Signature` | `t=<timestamp>,v1=<signature>`. `t` is the Unix time in seconds when the request was signed. `v1` is the HMAC-SHA256 of `<t>.<raw body>`, keyed with your app's client secret and hex-encoded |
| `Easyparcel-Webhook-Id` | ID of the event. It stays the same when the event is retried or resent, so you can use it to ignore an event you have already processed |
| `Easyparcel-Client-Id` | Client ID of the app the webhook belongs to. If one endpoint serves several apps, use it to choose which client secret to verify with |

To verify a webhook:

1. Read the raw request body exactly as received, before parsing the JSON. Parsing and re-encoding the JSON can change the bytes, and the signature will no longer match.
2. Split `Easyparcel-Signature` on `,` to get `t` and `v1`.
3. Compute the HMAC-SHA256 of `t`, a `.` and the raw body, using your client secret as the key, and hex-encode it.
4. Compare the result with `v1` using a constant-time comparison. If they differ, reject the request.
5. Reject the request if `t` is more than 5 minutes from your current time, so an old request cannot be sent to you again. Every retry is signed again with a new `t`.

> Verify a webhook signature:

```shell
# The raw request body is saved in body.json
t="1764208800"                # t from Easyparcel-Signature
v1="paste-the-v1-value-here"  # v1 from Easyparcel-Signature

expected=$( { printf '%s.' "$t"; cat body.json; } | openssl dgst -sha256 -hmac "$EASYPARCEL_CLIENT_SECRET" | sed 's/^.*= //')
[ "$expected" = "$v1" ] && echo "valid" || echo "invalid"
```

```javascript
const crypto = require('crypto');
const express = require('express');

const app = express();
const CLIENT_SECRET = process.env.EASYPARCEL_CLIENT_SECRET;

// express.raw keeps the body as bytes: the signature covers the body exactly as sent.
app.post('/webhook', express.raw({ type: 'application/json' }), (req, res) => {
  const rawBody = req.body.toString('utf8');
  const parts = Object.fromEntries(
    (req.get('Easyparcel-Signature') || '').split(',').map((part) => part.split('='))
  );

  const expected = crypto
    .createHmac('sha256', CLIENT_SECRET)
    .update(`${parts.t}.${rawBody}`)
    .digest('hex');
  const valid = typeof parts.v1 === 'string' && parts.v1.length === expected.length
    && crypto.timingSafeEqual(Buffer.from(parts.v1), Buffer.from(expected));
  const fresh = Math.abs(Date.now() / 1000 - Number(parts.t)) <= 300;

  if (!valid || !fresh) {
    return res.sendStatus(401);
  }

  const event = JSON.parse(rawBody);
  // Handle event.topic here
  res.sendStatus(200);
});

app.listen(3000);
```

```php
<?php
$clientSecret = getenv('EASYPARCEL_CLIENT_SECRET');
$rawBody = file_get_contents('php://input');

$parts = [];
foreach (explode(',', $_SERVER['HTTP_EASYPARCEL_SIGNATURE'] ?? '') as $part) {
    [$key, $value] = array_pad(explode('=', $part, 2), 2, '');
    $parts[$key] = $value;
}
$t = $parts['t'] ?? '';

$expected = hash_hmac('sha256', $t . '.' . $rawBody, $clientSecret);
$valid = hash_equals($expected, $parts['v1'] ?? '');
$fresh = ctype_digit($t) && abs(time() - (int) $t) <= 300;

if (!$valid || !$fresh) {
    http_response_code(401);
    exit;
}

$event = json_decode($rawBody, true);
// Handle $event['topic'] here
http_response_code(200);
```

```python
import hashlib
import hmac
import os
import time

from flask import Flask, abort, request

app = Flask(__name__)
CLIENT_SECRET = os.environ["EASYPARCEL_CLIENT_SECRET"].encode()


@app.post("/webhook")
def webhook():
    raw_body = request.get_data()  # the body exactly as sent, before JSON parsing
    header = request.headers.get("Easyparcel-Signature", "")
    parts = dict(part.split("=", 1) for part in header.split(",") if "=" in part)
    t = parts.get("t", "")

    expected = hmac.new(CLIENT_SECRET, t.encode() + b"." + raw_body, hashlib.sha256).hexdigest()
    valid = hmac.compare_digest(expected, parts.get("v1", ""))
    fresh = t.isdigit() and abs(time.time() - int(t)) <= 300

    if not valid or not fresh:
        abort(401)

    event = request.get_json()
    # Handle event["topic"] here
    return "", 200
```

<aside class="notice">
Requests also carry an older <code>Easyparcel-Hmac-SHA256</code> header. It is deprecated and will be removed. Its value is the same on every request and does not depend on the body, so it cannot prove a request is genuine. Use <code>Easyparcel-Signature</code> instead.
</aside>

<h2 id="usage-notes-webhook-2026-09">Usage Notes for Webhooks </h2>

- **Multiple Subscriptions**: You can subscribe to multiple topics for the same endpoint
- **Event Filtering**: Choose only the topics relevant to your application to reduce unnecessary webhook calls


<h2 id="important-notes-webhook-2026-09">Important Notes for Webhooks</h2>

- **Endpoint Requirements**: Your URL must be publicly accessible and able to handle POST requests
- **Multiple Topics**: You can subscribe to multiple webhook topics for the same endpoint
- **Payload Format**: All webhooks send a JSON body (`Content-Type: application/json`) with a `topic` field
- **Signature**: Every webhook is signed. Verify the `Easyparcel-Signature` header before you trust the payload (see [Verifying Webhook Signatures](#webhook-signature-2026-09))
- **Response Expected**: Your endpoint must return HTTP 200 within 3 seconds to acknowledge receipt (see [Delivery and Retries](#webhook-delivery-retries-2026-09))

### Testing Your Webhook

After setup, verify your webhook is working:
1. Trigger a test event in your app
2. Check your endpoint logs for incoming requests
3. Verify the payload structure matches your expectations
4. Ensure your endpoint responds with HTTP 200

### 🛠️ Troubleshooting for webhooks

**Common Issues:**
- **Endpoint not receiving data**: Verify URL is publicly accessible
- **SSL/HTTPS required**: Ensure your endpoint uses HTTPS
- **Timeout errors**: Your endpoint must respond within 3 seconds
- **Repeated deliveries**: Your endpoint returned something other than HTTP 200, so the event was retried
- **Signature does not match**: Compute it over the raw request body, not over JSON you have parsed and re-encoded, and use the client secret of the app in `Easyparcel-Client-Id`
