<html>
<head>
  <style>
    body {
      font-family: Arial, sans-serif;
      transition: background-color 0.3s, color 0.3s;
    }

    /* Default Light Mode */
    body.light-mode {
      background-color: #ffffff;
      color: #333333;
    }

    /* Dark Mode */
    body.dark-mode {
      background-color: #121212;
      color: #eaeaea;
    }

    .toggle-btn {
      position: absolute;
      top: 10px;
      right: 10px;
      padding: 10px;
      cursor: pointer;
      background-color: #007bff;
      color: white;
      border: none;
      border-radius: 5px;
    }

    .toggle-btn:hover {
      background-color: #0056b3;
    }
  </style>
</head>
<body class="light-mode">
  <button class="toggle-btn" onclick="toggleMode()">Toggle Dark/Light Mode</button>

  <!-- Your content goes here -->
  <p align="center">
    <img src="Pictures/easyparcel-transparentqquare-md.png" alt="Logo" style="width:250px;">
  </p>

  <h1>Easy Parcel API</h1>
  <p>The EasyParcel API allows your application to access current data within EasyParcel...</p>

  <!-- More of your content here -->

  <script>
    function toggleMode() {
      const currentMode = document.body.classList.contains('light-mode') ? 'light' : 'dark';
      if (currentMode === 'light') {
        document.body.classList.remove('light-mode');
        document.body.classList.add('dark-mode');
      } else {
        document.body.classList.remove('dark-mode');
        document.body.classList.add('light-mode');
      }
    }
  </script>
</body>
</html>
<p align="center">
<img src="Pictures/easyparcel-transparentqquare-md.png" alt="Logo" style="width:250px;">
</p>


# Easy Parcel API  

 
The EasyParcel API allows your application to access current data within EasyParcel. However, EasyParcel API is using RESTful to develop API for web based applications. Through the API, several common operations can be performed on EasyParcel objects.

---

## Table of Contents 
- [Guides](#Guides)
- [Oauth](#Oauth-Authentication)
- [Features](#API-Functions-Features)
- [Order Flow](#Order-function-Flow)
- [References](#References)

---

### Guides
#### Follow the guide below to integrate with easy parcel api.

#### [Steps to get started with EASYPARCEL](Guides/1.get_started_with_EASY_PARCEL_OPEN_API.md)
#### [Setup Demo Account](Guides/2.setup_demo_account.md)
#### [Get Oauth Access token](Guides/3.get_Oauth_Access_token.md)

---
### Oauth Authentication

EasyParcel's API employs the OAuth 2.0 authorization framework to provide secure and controlled access to its services.

#### [More about Oauth Authentication](oauth_authentication.md)
#### [Steps to get Oauth Access token](Guides/3.steps_to_get_oauth_access_token.md)
---

### API Functions Features

#### [Functions/Features](Features/README.md)


#### Standard

[Get Shipment Quotation](Features/Shipping/1.get_shipment_quotation.md)

[Get Insurance Quotation](Features/Shipping/2.get_insurance_quotation.md)

[Get Courier Dropoff point](Features/Shipping/3.get_courier_dropoff_point.md)

[Submit Shipment Orders](Features/Shipping/4.submit_shipment_orders.md)

#### OnDemand

[Get OnDemand Quotation](Features/OnDemand/1.get_ondemand_quotation.md)

[Submit OnDemand Order](Features/OnDemand/2.submit_ondemand_order.md)

#### Wallet

[Get Wallet](Features/get_wallet.md)

---

### Order function Flow
<img src="Pictures/flow_chart.png" alt="Flow Chart" style="width:40%; margin:0; padding:0;">

---

### References

**[API Return Status](References/API_return_status.md)**

**[Conutry Code](References/country_code.md)**

**[ISO 3166](References/ISO_3166.md)**
