# <span style="color: blue;"> OnDemand Shipping</span> 

## OnDemand API Flow Overview

This document provides a visual representation of the different flows and processes available through the EasyParcel API.

### OnDemand Workflow Diagram

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
