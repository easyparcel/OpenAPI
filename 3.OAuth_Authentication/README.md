# OAuth 2.0 Authentication

EasyParcel uses **OAuth 2.0** to securely authenticate API requests. This method allows third-party applications to interact with EasyParcel APIs without exposing user credentials directly.

---

## 📌 What is OAuth 2.0?

OAuth 2.0 is an industry-standard protocol for authorization. It enables applications to obtain limited access to user accounts on an HTTP service without sharing password data.

In EasyParcel’s case, it allows you to access API features by exchanging a **Client ID** and **Client Secret** for a temporary **Access Token**.

---

## 🔐 How Authentication Works

1. **Register your app**  
   - You’ll receive a `client_id` and `client_secret`.

2. **Request an access token**  
   - Send a `POST` request to the EasyParcel token URL:
     ```
     POST https://api.easyparcel.com/auth/token
     ```

3. **Use the token in API calls**  
   - Include it as a Bearer token in your request headers:
     ```
     Authorization: Bearer YOUR_ACCESS_TOKEN
     ```

4. **Token Expiry**  
   - Tokens are valid for a limited time. Re-authenticate to get a new one as needed.

---

## 🧪 Example: Get Access Token

**Request:**

```http
POST /auth/token
Host: api.easyparcel.com
Content-Type: application/x-www-form-urlencoded

client_id=YOUR_CLIENT_ID
&client_secret=YOUR_CLIENT_SECRET
&grant_type=client_credentials
