# <span style="color: black;"> Sandbox Account </span>

The EasyParcel **sandbox account** is a test environment designed for developers and integrators to simulate real-world usage of EasyParcel's API features without affecting live production data.


## 🔍 Key Highlights

* **Free to use**: The sandbox environment and test credits are completely free.
* **Safe testing**: You can freely test all API operations (like quotations, order submission, cancellation, etc.) without risk to your live account.
* **Test credits available**: You can simulate order submissions with test credits.
* **Live account unaffected**: No changes or charges are applied to your actual EasyParcel account.


## Use cases
### Ideal For

* Testing API integrations before go-live
* QA and staging environments
* Training or demonstrations


For top up test credits instructions, please refer to the [Top up Sandbox Credit](#top-up-demo-account) guide.

Sandbox Limitation:
refer here for [Sandbox Limitations](#sandbox-limitations) 


## Demo Account Setup Guide

### Prerequisites
- Existing EasyParcel developer account
- Completed API application registration
- Client ID credentials


### Step-by-Step Demo Account Setup

#### 1. Access Developer Portal
**URL:** [https://api.easyparcel.com](https://api.easyparcel.com)  
<p align="center">
  <img src="https://github.com/user-attachments/assets/287ae19b-3d27-4751-b2fb-96f58f9c89ae"
       alt="image"
       style="max-width: 105%; height: auto;" />
</p>





#### 2. Select Application
**Action:** Choose your registered application from the dashboard  
<p align="center">
<img alt="image" src="https://github.com/user-attachments/assets/b30ce194-3b8d-4d90-9c2f-eb885bccb5ab" alt="image" style="max-width: 105%; height: auto;" />
</p>


#### 3. Navigate to Connections
**Location:** Settings → Connection Management  
<p align="center">
<img width="1192" height="592" alt="image" src="https://github.com/user-attachments/assets/2a72d5f9-a706-423f-845c-4a5e6719898e" alt="image" style="max-width: 105%; height: auto;" />
</p>


#### 4. Add New Connection
**Required:**  
✅ Sandbox environment selection  
✅ Connection name  
<p align="center">
<img width="2560" height="714" alt="image" src="https://github.com/user-attachments/assets/c8cb387a-1f2e-4cdc-b658-3bc1010938cc" alt="image" style="max-width: 105%; height: auto;" />
</p>


#### 5. Prompt to login
**Required:**  
Login using developers account credentials
<p align="center">
<img width="1232" height="1276" alt="image" src="https://github.com/user-attachments/assets/f97d0d40-6efd-4d97-a723-544e5cf70144" alt="image" style="max-width: 105%; height: auto;"/>
</p>


#### 6. Allow access request
**Required:**  
Allow the application request to access account credentials and permisions
<p align="center">
<img width="1230" height="816" alt="image" src="https://github.com/user-attachments/assets/975ef6b7-f38d-403c-84cb-67e5b9ba88a5" alt="image" style="max-width: 105%; height: auto;"/>
</p>


#### 7. Verify Successful Setup
**Confirmation:** Look for active status indicator  
<p align="center">
<img width="2556" height="706" alt="image" src="https://github.com/user-attachments/assets/a128d3be-45f8-4827-a054-7e8f151dfdcc" alt="image" style="max-width: 105%; height: auto;"/>
</p>


## Top up demo account

1. In the Application settings, connection list, select **Top Up**
<p align="center">
<img width="2538" height="746" alt="image" src="https://github.com/user-attachments/assets/9d5e7d15-67f0-41fc-a165-fc92bd99c947" alt="image" style="max-width: 105%; height: auto;"/>
</p>

3. Top up the desired amount
<p align="center">
<img width="2560" height="900" alt="image" src="https://github.com/user-attachments/assets/ab458b36-6b43-4b87-9f06-d13a6367ae69" alt="image" style="max-width: 105%; height: auto;"/>
</p>

5. Top up successful
<p align="center">
<img width="2560" height="744" alt="image" src="https://github.com/user-attachments/assets/5212a32d-903a-486a-a766-fc562a701e6c" alt="image" style="max-width: 105%; height: auto;"/>
</p>


## Sandbox Limitations

While the EasyParcel **sandbox environment** allows full API integration testing, there are several limitations compared to the live environment.


### ⚠️ Key Limitations

* **Shipment status will not update**

   Any shipment created in the sandbox will remain static — it will not progress through actual delivery stages.

* **No tracking notifications**

   Add-on features such as SMS, email, and WhatsApp tracking notifications will not be triggered or sent.



Use the sandbox for development and testing purposes. For real transactions and shipment tracking, switch to the production environment.

## Switching to live
You wish to perform live order [live account](#switching-to-live)
