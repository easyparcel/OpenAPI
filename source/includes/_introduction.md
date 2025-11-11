# <span style="color: black;"> Introduction </span>
# <span style="color: black;"> EasyParcel API Documentation </span>

Welcome to the **EasyParcel API Documentation**! This guide will help you integrate with EasyParcel and get access to shipping functionalities via a RESTful API interface. 


## **Overview**

The **EasyParcel API** enables you to manage shipping, obtain quotations, track shipments, and much more. It's designed using a RESTful architecture, offering a seamless integration with various e-commerce platforms and third-party applications.

### **Key Benefits**:
- **Rate Calculation**: Get live rates from various couriers.
- **Order Management**: Create, update, and manage shipments.
- **Tracking**: Real-time tracking updates for shipments.
- **Effortless APP Integrate**: Easy integration with your online store or application.

## **Setup Flow**

Below is a visual guide to set up flow:
<p align="center">
<img alt="image" style="max-width: 105%; height: auto;" src="https://github.com/user-attachments/assets/89d588d1-1d17-4b17-baed-f418789ad916" />
</p>


## **Getting Started**

To begin using the EasyParcel API, follow the steps below to set up your environment:

- [Register Developer account](#Developer-Hub)
- [Register Developer account](#Developer-Hub)
- [Create Sandbox account](#sandbox-account)
- [Oauth](#oauth-2-0)
- [Postman_collections](#postman-collection)
- [API Endpoint](#api-functions-amp-features)
- [Webhook](#webhooks)

Once set up, you can use the provided **Sandbox** environment to test the API without impacting live data.



## **OAuth Authentication**

EasyParcel uses **OAuth 2.0** for secure authentication, enabling controlled access to the system.

1. **OAuth 2.0 Overview**:
    - OAuth 2.0 is a standard authorization framework allowing third-party applications to access your EasyParcel resources without exposing sensitive credentials.
  
2. **Steps to Obtain OAuth Token**:
    - [Learn about OAuth Authentication](#oauth-authentications)
    - [Getting OAuth Access Token](#get-oauth-access-token)


## **API Functions & Feature**

The EasyParcel API offers a wide array of functionalities divided into categories. Below are the key features available:

### **Standard Features**:
- **Get Shipment Quotation**  
  Get a detailed quote for your shipment, including rates, delivery times, and courier options.  
  [Read more](#shipment-quotations)

- **Get Coupon List**  
  Fetch all available courier according to the country.
  [Read more](#coupon-feature)

- **Submit Shipment Orders**  
  Create and submit shipment orders for processing.  
  [Read more](#submit-orders)

### **OnDemand Features**:
- **Get OnDemand Quotation**  
  Get an on-demand quotation based on specific criteria.  
  [Read more](#ondmeand-quotation)

- **Submit OnDemand Order**  
  Create an on-demand shipment order.  
  [Read more](#ondemand-order-submission)

### **Wallet Features**:
- **Get Wallet Balance**  
  Check your current wallet balance for API transactions.  
  [Read more](#wallet-balance)


#### **Contact Us**

If you have any questions or need further support with the EasyParcel API, our team is available for assistance. You can reach out to us via the following channels:
- **WhatsApp Support**: For quick support, chat with our team directly on WhatsApp. Click [here](https://wa.me/6042023160) to start a conversation.

We’re here to help you integrate and make the most out of EasyParcel’s services!
