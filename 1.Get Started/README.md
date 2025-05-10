UNDERSTAND BASIC FLOW OF EASYPARCEL OPEN API
# Getting Started with EasyParcel Open API

Welcome! This guide will help you get started with integrating EasyParcel's Open API into your application or platform.

## 1. Prerequisites

Before you begin, make sure you have:
- A registered EasyParcel account
- Access to EasyParcel's **Developer Portal** or API credentials
- Basic understanding of REST APIs
- Tools like Postman or cURL for testing API calls

## 2. Sandbox vs Live

- **Sandbox**: For testing purposes. No credits will be deducted.
- **Live**: For real transactions. Ensure you have sufficient wallet balance.

## 3. Authentication

EasyParcel uses **OAuth 2.0**. Before making API calls, you must:
- Register your application with EasyParcel
- Obtain `client_id` and `client_secret`
- Request an **access token** using those credentials

Refer to the [OAuth Authentication Guide](../3.OAuth_Authentication/1.oauth_authentication.md) for more details.

## 4. Basic API Workflow

1. **Get Access Token**  
   → Authenticate and receive a bearer token.

2. **Check Wallet Balance (optional)**  
   → Ensure sufficient credits for certain operations.

3. **Get Quotation**  
   → Determine available couriers and costs.

4. **Submit Shipment Order**  
   → Create a shipment based on selected courier and package details.

5. **Track Shipment**  
   → Use tracking API to monitor delivery status.

## 5. Useful Resources

- [Setup a Demo Account](../2.Integration/setup_demo_account.md)
- [Quotation API](../Features/Shipping/1.get_shipment_quotation.md)
- [Submit Shipment Orders](../Features/Shipping/4.submit_shipment_orders.md)

---

Happy shipping! For assistance, reach out to [EasyParcel Support](https://wa.me/6042023160).
