# <span style="color: black;"> Webhooks </span>
## 🔗 How to Subscribe to Webhooks

### 📋 Prerequisites

Before setting up webhooks, ensure you have:
- An active EasyParcel developer account
- A configured app in the Developer Hub
- A valid endpoint URL that can receive POST requests
- Your endpoint configured to handle webhook payloads

## 🛠️ Subscription Steps

Follow these steps to subscribe to webhooks:

### 1. 🎯 Navigate to App Settings
- Go to **Developer Hub Dashboard**
- Click on **Apps**
- Select **Settings** on the app you wish to configure webhooks for
<img width="1145" height="401" alt="image" src="https://github.com/user-attachments/assets/a9559156-b73e-4e1a-88c9-dd4da2438600" />

### 2. 📡 Access Webhook Configuration
- In the left sidebar, click **Webhook**
- Click the **Add Endpoint** button
<img width="1026" height="231" alt="image" src="https://github.com/user-attachments/assets/37f9c760-009a-414b-b2da-a2f218861dab" />

### 3. ⚙️ Configure Webhook Details
- **Enter Endpoint URL**: Input the URL that will receive the webhook payload
- **Select Webhook Topic**: Choose the event(s) you want to subscribe to from the available options
- **Verify Configuration**: Double-check your URL and selected topics
<img width="285" height="186" alt="image" src="https://github.com/user-attachments/assets/22b0dbc1-9c1a-4e46-8827-1cb350eb2e57" />

### 4. 💾 Save Configuration
- Press **Save** to confirm your webhook settings
- Your webhook endpoint will be validated

### 5. ✅ Confirmation
- **Done!** Your webhook is now active and will be triggered according to your selected topics
- Test your endpoint to ensure it's receiving webhook data correctly


## 📋 Webhook Topics

| Topic ID | Webhook Topic Name | Description |
|----------|-------------------|-------------|
| 1 | Ondemand Order Status Update | Triggered when an on-demand order status changes |
| 2 | Shipment Status Update | Triggered when a shipment status changes |
| 3 | Shipment AWB Update | Triggered when a shipment AWB (Air Waybill) is updated |
| 4 | Tracking Status Update | Triggered when package tracking status is updated |
| 5 | Shipment Created | Triggered when a new shipment is created |

## Webhook Sample Payload:

```json
//Shipment Status Update Sample:
        {
            "topic": "shipment.awb.update",
            "shipment_number": "ES-2504-G7FDF",
            "uuid": "webhook-test-uuid-123",
            "timestamp":"2017-10-28 11:40:00",
            "awb_number": "238725129086",
            "awb_url":"http:\/\/demo.connect.easyparcel.my\/?ac=AWBLabel&id=QmIxTE43eHQjMTYzMDQwMTI%3D",
            "tracking_url":"https:\/\/easyparcel.com\/my\/en\/track\/details\/?courier=Skynet&awb=23877001523"
        }
```

```json
//Shipment AWB Update Sample:
        {
            "topic": "shipment.awb.update",
            "shipment_number": "ES-2504-G7FDF",
            "uuid": "webhook-test-uuid-123",
            "timestamp":"2017-10-28 11:40:00",
            "awb_number": "23872512999",
            "awb_url":"http:\/\/demo.connect.easyparcel.my\/?ac=AWBLabel&id=QmIxTE43eHQjMTYzMDQwAAA%3D",
            "tracking_url":"https:\/\/easyparcel.com\/my\/en\/track\/details\/?courier=Skynet&awb=23877001999"
        }
```

```json
//Shipment AWB Update Sample:
    {

        "topic": "shipment.tracking.update",
        "shipment_number": "ES-2504-G7FDF",
        "uuid": "webhook-test-uuid-123",
        "timestamp":"2017-10-28 11:40:00",
        "awb_number": "238725129086",
        "latest_shipment_status_code":5,
        "latest_tracking_status": "Deliverd To Suntech",
        "timestamp":"2017-10-28 11:40:00",
        "status_log":[
            "0":{
            "timestamp":"2017-10-28 11:40:00",
            "shipment_status_code":5,
            "tracking_status" : "Deliverd To Suntech"
            },
            "1":{
            "timestamp":"2017-06-28 12:00:00",
            "shipment_status_code":3,
            "tracking_status":"Parcel has been collected at Penang"
            }
        ]
    }
```

```json
//Shipment Create Sample:
        {
            "shipment_number": "WEBHOOK-TEST-001",
            "uuid": "webhook-test-uuid-123",
            "timestamp":"2017-10-28 11:40:00",
            "sender_name": "Test Sender",
            "receiver_name": "Test Receiver",
            "sender_phone_number": "0123456789",
            "receiver_phone_number": "0987654321",
            "sender_email": "sender@test.com",
            "receiver_email": "receiver@test.com",
            "sender_address1": "Test Address 1",
            "receiver_address1": "Test Address 1",
            "sender_postcode": "12345",
            "receiver_postcode": "54321",
            "sender_city": "Test City",
            "receiver_city": "Test City",
            "sender_country_code": "MY",
            "receiver_country_code": "MY",
            "weight": 1.0,
            "length": 10,
            "width": 10,
            "height": 10,
            "service_id": 1,
            "courier_id": 1,
            "status": 1
        }
```

```json
//Ondemand Order Status Update Sample:
    {
        "topic": "ondemand.status.update",
        "order_number": "EODWEBHOOK-TEST-001",
        "tracking_url": "https:\/\/easyparcel.com\/my\/en\/track\/details\/?courier=Skynet&awb=23877001523",
        "status": 0,
        "timeline": ,
        "driver": { 
            "id": "81994", "name": "TestDriver 09090", "phone": "+6090909090",   "photo": "", "rating": "", "vehicle": {"model": "", "licensePlate": "VP5734736", "physicalVehicleType": "Bike"}, "coordinates": {"latitude": 0, "longitudelatitude": 0 }
        },
        "event_date": "2025-06-06 04:21:07",
        "waypoint": [
            {"pod": null, "coordinate": {"latitude": 5.325513957, "longitude": 100.2862732}}, 
            {"pod": "http://sg-oimg-pre.lalamove.com/appdriver/pre/appdriver/2021/07/05/1625479646347738192598.png", "coordinate": {"latitude": 5.325513957, "longitude": 100.2862732}}
            ],
    }
```

##  Usage Notes for webhooks

- **Multiple Subscriptions**: You can subscribe to multiple topics for the same endpoint
- **Event Filtering**: Choose only the topics relevant to your application to reduce unnecessary webhook calls


## 📝 Important Notes for webhooks

- **Endpoint Requirements**: Your URL must be publicly accessible and able to handle POST requests
- **Multiple Topics**: You can subscribe to multiple webhook topics for the same endpoint
- **Payload Format**: All webhooks send JSON payloads with event-specific data
- **Response Expected**: Your endpoint should return a 200 status code to acknowledge receipt
- **Retry Logic**: Failed webhook deliveries may be retried automatically

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
- **Timeout errors**: Your endpoint should respond quickly (within 30 seconds)
- **Invalid responses**: Return proper HTTP status codes

