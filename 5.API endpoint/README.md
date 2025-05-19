### **API Functions & Features**

The EasyParcel API offers various functionalities grouped under different categories. Below is an overview of the key features:

#### **Standard Shipping**:
- Scheduled Delivery

- Cost-effective

- Tracking Available

- Suitable for high volume shipment

#### **OnDemand Shipping**:

- Speed: providing same-day delivery.

- Real-Time Tracking: You can track your parcel in real-time once the booking is made.

- Flexibility: You can choose your preferred vehicle and schedule the pick-up time.

- Cost-Efficiency: You only pay for the services you need.

- Priority Handling: Parcels are prioritized, ensuring faster delivery compared to standard methods.

#### **Wallet**:
- All submission will be deducting from credit waller

#### **Get Courier List**:
- Getting all the courier listing available for a country

#### **Get Coupon List**:
- Getting coupon available for the order for both standard shipping and ondemand

---

# EasyParcel API Flow Overview

This document provides a visual representation of the different flows and processes available through the EasyParcel API.

## API Workflow Diagram

```mermaid
graph TD
    A[[EasyParcel API]] --> B[[Shipping]]
    A --> C[[Ondemand]]
    A --> D[[General Services]]
    
    %% Shipping Flow
    B --> B1[[Order Flow]]
    B --> B2[[Listing Flow]]
    
    %% Order Flow
    B1 --> B11[Get Quotation]
    B11 --> B12[Get Cuopon Listing]
    B12 --> B13[Submit Order]
    
    %% Listing Flow
    B2 --> B21[Get Shipment Listing]
    B21 --> B22[Get Shipment Details]
    B22 --> B23[Cancel Orders]
    
    %% Ondemand Flow
    C --> C1[[Ondemand Order Flow]]
    C1 --> C2[Get Ondemand Quotation]
    C2 --> C3[Get Ondemand Coupon Listing]
    C3 --> C4[Submit Ondemand Orders]
    C4 --> C5[Cancel Order]
    
    %% General Services
    D --> D1[Courier Listing]
    D --> D2[[Credit Wallet Flow]]
    D2 --> D21[Get Credit Wallet]
```
### **Order Function Flow**

Here’s a visual representation of the order function flow in the EasyParcel API:

<p align="center">
  <img src="../8.Picture/5.API endpoint/flow_chart.png" alt="Order Flow Chart" style="width:50%; margin:0; padding:0;">
</p>

---


### [Shipping](Shipping)
  
[Get Shipment Quotation](1.Shipping/1.get%20shipment%20quotation.md)

[Coupon Listing](1.Shipping/3.Coupon.md)

[Submit Shipment Order](1.Shipping/2.Submit%20Orders.md)

[Get Shipment Listing](1.Shipping/3.Get%20Shipment%20Listing.md)

[Get Shipment Details](1.Shipping/4.Get%20Shipment%20details.md)

[Cancel Order](/1.Shipping/5.Cancel%20Shipment.md)



### [OnDemand](OnDemand)

[Get OnDemand Quotation](%202.Ondemand/1.Get%20Ondemand%20Quotation.md)

[Coupon Listing](%202.Ondemand/2.Coupon.md)

[Submit OnDemand Order](%202.Ondemand/2.Submit%20Ondemand%20Order.md)

[Cancel OnDemand Order](%202.Ondemand/3.Cancel%20Ondemand.md)


### Wallet

[Get Wallet](3.Get%20Credit%20Wallet.md)


### Courier List
[Courier Listing](4.Courier%20listing.md)




<div align="center" style="margin: 1.5rem 0;">

[![Back to official documents](https://img.shields.io/badge/Back_to_official_documents-007ACC?style=flat-square)](../README.md)


</div>
