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
            "event_date": "2025-04-26 12:00:00",
            "shipment_status_code": 3,
            "tracking_status": "Parcel has been collected at Penang"
        },
        "1": {
            "event_date": "2025-04-28 11:40:00",
            "shipment_status_code": 5,
            "tracking_status": "Delivered to recipient"
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
| status_log | object | Every tracking event so far, keyed `"0"`, `"1"`, … from oldest to newest. Each has `event_date`, `shipment_status_code` and `tracking_status` |
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

<h2 id="webhook-verify-2026-09">Verifying That a Webhook Came From EasyParcel</h2>

Every webhook request carries this header:

| Header | Value |
|--------|-------|
| `Easyparcel-Hmac-SHA256` | The SHA-256 hash of your app's **Client Secret** (shown in Developer Hub → Apps → Settings), as lowercase hex |

To check it, compute the SHA-256 of your Client Secret once, then compare it with the header on each request using a constant-time comparison. Reject requests where it doesn't match.

```javascript
const crypto = require('crypto');

const expected = crypto.createHash('sha256').update(process.env.EP_CLIENT_SECRET).digest('hex');

function isFromEasyParcel(req) {
  const received = req.get('Easyparcel-Hmac-SHA256') || '';
  return received.length === expected.length &&
    crypto.timingSafeEqual(Buffer.from(received), Buffer.from(expected));
}
```

```php
<?php
$expected = hash('sha256', getenv('EP_CLIENT_SECRET'));
$received = $_SERVER['HTTP_EASYPARCEL_HMAC_SHA256'] ?? '';
if (!hash_equals($expected, $received)) {
    http_response_code(401);
    exit;
}
```

<aside class="warning">
The header value is the same on every request: it is derived from your Client Secret only and does not sign the request body. It shows that the sender knows your secret. It does not prove the payload is unchanged. For actions that matter (fulfilling an order, releasing goods, refunds), also:
<ul>
<li>use an HTTPS endpoint, and keep its URL private;</li>
<li>treat the webhook as a signal, and fetch the current state from the API (for example <code>POST /shipment/details</code> or <code>POST /shipment/tracking_status</code>) before acting on it.</li>
</ul>
</aside>

<h2 id="webhook-delivery-retries-2026-09">Delivery and Retries</h2>

- **Timeout**: EasyParcel waits **3 seconds** for your endpoint to respond. Reply quickly, and do any slow work after you have responded.
- **Success**: only an HTTP **200** response counts as delivered. Any other status code (including `201`, `202` and `204`), a timeout or a connection error counts as a failure.
- **Retries**: a failed delivery is retried up to **3 times**, about 5, 10 and 20 minutes after the first attempt. After that the event is not sent again automatically.
- **Duplicates and order**: the same event can arrive more than once, and events can arrive out of order. Use `shipment_number` / `order_number` with `topic` and `event_date` to ignore duplicates and older updates.

<h2 id="usage-notes-webhook-2026-09">Usage Notes for Webhooks </h2>

- **Multiple Subscriptions**: You can subscribe to multiple topics for the same endpoint
- **Event Filtering**: Choose only the topics relevant to your application to reduce unnecessary webhook calls


<h2 id="important-notes-webhook-2026-09">Important Notes for Webhooks</h2>

- **Endpoint Requirements**: Your URL must be publicly accessible and able to handle POST requests
- **Multiple Topics**: You can subscribe to multiple webhook topics for the same endpoint
- **Payload Format**: All webhooks send a JSON body (`Content-Type: application/json`) with a `topic` field
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
