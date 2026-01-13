<h1 id=od-shipping-2025-06"><span style="color: blue;"> On-demand Shipping </span></h1>

<h2 id="od-API-flow-2025-06"> Ondemand API Flow Overview</h2>

This document provides a visual representation of the different flows and processes available through the EasyParcel API.

### Ondemand Workflow Diagram

```mermaid
graph TD
B[[Shipping]]
    %% Shipping Flow
    B --> B1[[Order Flow]]
    B --> B2[[Cancel Flow]]

    %% Order Flow
    B1 --> B11[Get Ondemand Quotation]
    B11 --> B12[Get Cuopon Listing]
    B12 --> B13[Submit Order]

    %% Cancel Flow
    B2 --> B23[Cancel Orders]
    
```
