# <span style="color: black;"> Developer Hub </span>
## 👨‍💻 Welcome to the EasyParcel Developer Hub

The **EasyParcel Developer Hub** is your one-stop destination for building and integrating custom shipping solutions using our API.

## Why Register on the Developer Hub?

The EasyParcel Developer Hub is the central portal for developers who want to integrate with our API. Registration is required to:

- Create and manage OAuth applications
- Generate authentication credentials (client ID and client secret)
- Access API documentation and resources
- Test API endpoints in a sandbox environment
- Monitor API usage and performance

## 🚀 What You Can Do Here

* **Create and manage your apps** to access EasyParcel's APIs securely.
* **Integrate with our Open API** for features like quotations, order submissions, and tracking.
* **Subscribe to Webhooks** to receive real-time shipment updates.
* **Test with a Sandbox Account** that includes free test credit and no impact on your live data.

Whether you're developing a plugin, connecting your e-commerce store, or building a custom logistics tool — the Developer Hub has everything you need to get started.



## Registering on the EasyParcel Developer Hub

This guide provides step-by-step instructions for registering on the EasyParcel Developer Hub and setting up your application to access the EasyParcel API.


## Registration Process

### Step 1: Create a Developer Account

1. Visit the [EasyParcel Developer Hub](https://api.easyparcel.com) and login

<p align="center">
  <img src="https://github.com/user-attachments/assets/b44f03b0-4925-4273-86cd-1b125645ebde"
       alt="Screenshot 2025-11-11 at 5 27 38 PM"
       style="max-width: 105%; height: auto;">
</p>

2. Login or sign up easyparcel developer account.  
   *You already singed up, you may proceed to login (skipped to step 2)*

   Click on the **Sign Up**

<p align="center">
  <img src="https://github.com/user-attachments/assets/f5d9b21a-c283-4701-aba3-ffbb0cda8ded"
       alt="image"
       style="max-width: 105%; height: auto;">
</p>

Complete the registration form:
- Full name  
- Email address  
- Password (must be at least 8 characters with numbers and special characters)  
- Company name  
- Contact number

<p align="center">
  <img src="https://github.com/user-attachments/assets/baac6130-8ebb-436c-987f-cec9501656fa"
       alt="image"
       style="max-width: 105%; height: auto;">
</p>

3. Accept the Terms of Service and Privacy Policy  
4. Click **Create Account**  
5. Verify your email address by clicking the link sent to your email  

### Step 2: Complete Your Developer Profile

After verifying your email and logging in, you'll need to complete your developer profile with the following information:

#### Basic Information
- **Account Name*** - Your developer account name (usually your company name)
- **Website** - Your company or personal website URL

#### Contact Information

EasyParcel will use this information to contact you about your account.

- **Contact Email*** - Primary email for account communications  
- **Phone Number*** - Contact phone with country code  
- **Address 1*** - Primary address  
- **Address 2** - Additional address information (optional)  
- **City*** - Your city  
- **ZIP / Postal Code*** - Your postal code  
- **State / Territory*** - Your state or territory  
- **Country*** - Your country

<p align="center">
  <img src="https://github.com/user-attachments/assets/9219aab6-9308-4a12-86df-4fac5011726c"
       alt="445981046-ac2be59f-0f9e-4190-99c2-8438d80718a4"
       style="max-width: 105%; height: auto;">
</p>




### Emergency Developer Contact Information
These details are used to communicate critical technical information to developers who maintain apps.

 **Emergency Developer Email*** - Email for urgent technical communications
  
 **Emergency Developer Phone Number*** - Phone for urgent technical communications

Fields marked with an asterisk (*) are required.

Once you've filled out all required fields, click **Save Profile** to continue.


If you encounter any issues during registration or application setup, contact our developer support team at api@easyparcel.com.

## Creating Easyparcel Application
### Create an Application

To access the API, you need to create an application:

1. In the Developer Hub dashboard, click on **Applications**
2. Click **Create New Application**

<p align="center">
  <img src="https://github.com/user-attachments/assets/ddb518b3-e6c5-4e46-82fb-34acc2d8a756"
       alt="image"
       style="max-width: 105%; height: auto;">
</p>

4. Fill in the application details:

   - Application name
   - Redirect URI (for OAuth flows)

<p align="center">
  <img src="https://github.com/user-attachments/assets/df84109c-b2ea-44b4-a22c-64169ec5e26b"
       alt="image"
       style="max-width: 105%; height: auto;">
</p>

## Understanding Redirect URI

The **Redirect URI** (also known as callback URL) is a crucial component of the OAuth 2.0 authentication flow. Here's what you need to know:

**What is a Redirect URI?**
A redirect URI is the URL in your application where Easy Parcel will send users after they successfully authenticate. It's essentially the "return address" for the OAuth flow.

**Why is it required?**

- **Security**: Ensures that authorization codes are only sent to pre-registered, trusted URLs
  
- **OAuth Compliance**: Required by OAuth 2.0 specification to prevent authorization code interception attacks
  
- **User Experience**: Provides a seamless flow back to your application after authentication
  

**How to configure your Redirect URI:**

**For Web Applications:**

https://yourdomain.com/auth/callback

https://yourapp.com/oauth/easyparcel/callback


**For Local Development:**

http://localhost:3000/auth/callback

http://127.0.0.1:8080/callback


**For Mobile Applications:**

yourapp://oauth/callback.com.yourcompany.yourapp://auth



## Once create the app

### Access Token Expiry Configuration
Easy Parcel allows you to configure the expiry time for access tokens based on your application's security requirements and user experience needs.

<p align="center">
  <img src="https://github.com/user-attachments/assets/342f75f4-db5e-4dae-aedd-fda5db2f561e"
       alt="image"
       style="max-width: 105%; height: auto;">
</p>


**What are Access Tokens?**
Access tokens are credentials that allow your application to access Easy Parcel's API on behalf of authenticated users. They have a limited lifespan for security purposes.

**Why Configure Token Expiry?**

- **Security**: Shorter expiry times reduce the risk if tokens are compromised

- **User Experience**: Longer expiry times reduce the frequency of re-authentication

- **Compliance**: Meet your organization's security policies and regulations

**How to Set Token Expiry:**
1. In your application settings, look for Access Token expiration
2. Select your preferred expiry duration from the dropdown
3. Consider your application type and security requirements
4. Save the configuration

**Best Practices by Application Type:**

**Web Applications:**

- **Recommended**: 1-4 hours

- **Rationale**: Balance between security and user experience

- **Implementation**: Use refresh tokens for seamless renewal

**Mobile Applications:**

- **Recommended**: 24 hours to 7 days

- **Rationale**: Reduces frequent login prompts on mobile devices

- **Implementation**: Implement background token refresh

**Server-to-Server Integrations:**

- **Recommended**: 1-24 hours

- **Rationale**: Automated systems can handle frequent token refresh

- **Implementation**: Automatic token renewal in your backend

**Public/Kiosk Applications:**
- **Recommended**: 15-60 minutes

- **Rationale**: Higher security risk in public environments

- **Implementation**: Frequent re-authentication acceptable



### Fill in the application details:
- description (optional)
- Application logo (optional)

<p align="center">
  <img src="https://github.com/user-attachments/assets/272ded5c-92b5-469f-82d8-8bafe02ee052"
       alt="445985136-7d47790d-64a5-4b11-acd0-f9bc3e6d1350"
       style="max-width: 105%; height: auto;">
</p>

### Once completed, congradulations! You have create your first app in easyparcel account!


## Get App Client credentials

### Step 3: Get Client credentials
1.)Get the client creditials for oauth authentication
  - client id
  - client secret

<p align="center">
  <img src="https://github.com/user-attachments/assets/1ca43169-d484-4704-bb40-deceb552e53b"
       alt="image"
       style="max-width: 105%; height: auto;">
</p>

2.)Follow [the Steps to get Oauth access token](#get-oauth-access-token)
