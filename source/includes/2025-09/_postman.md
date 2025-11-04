# <span style="color: black;"> Postman Collection </span>

## Getting Started

Our Postman collection provides a convenient way to explore and test the EasyParcel API endpoints. Follow these steps to get up and running quickly.

This guide helps you get started with the EasyParcel API using Postman, providing instructions for importing, configuring, and using our Postman collection.

## Importing the Collection
1. Download the collection JSON file from over [**Here**](https://github.com/easyparcel/OpenAPI/blob/2025-06/4.Postman%20Collection/Open%20API%202025-06.postman_collection.json)
2. Open Postman
3. Click **Import** in the top-left corner
4. Choose the **File** tab and select the downloaded JSON file
5. Click **Import**

## Configuration
Enter this redirect/call URL to your app, if you intent to use for postman
```
https://oauth.pstmn.io/v1/callback
```

<img width="553" alt="image" src="https://github.com/user-attachments/assets/5df94f95-341f-4291-91ea-fcd1dff64691" />

Before using the collection, you need to set up your environment variables:

1. Create a new environment in Postman
2. Add the following variables:
   - `baseUrl` - Set to `https://api.easyparcel.com`
   - `apiVersion` - Set to `open_api/2025-06`
   - `clientId` - Your EasyParcel OAuth client ID
   - `clientSecret` - Your EasyParcel OAuth client secret


## Authentication

The EasyParcel API uses OAuth 2.0 for authentication. The collection is pre-configured with the necessary OAuth settings:

1. In Postman, open the collection and click on the **Authorization** tab
2. Verify that the authorization type is set to **OAuth 2.0**
3. Click on **Get New Access Token** and follow these steps:
   - **Grant Type**: Authorization Code
   - **Auth URL**: https://developer.easyparcel.com/oauth/login
   - **Access Token URL**: https://api.easyparcel.com/oauth/token
   - **Client ID**: Your EasyParcel client ID
   - **Client Secret**: Your EasyParcel client secret
   - **Scope**: (leave as is or use specific scopes if provided)
4. Click **Request Token**
5. Once you receive the token, click **Use Token**


The collection will automatically include the token in all requests.


<img width="799" alt="Screenshot 2025-05-26 at 9 27 41 AM" src="https://github.com/user-attachments/assets/d37cd541-639c-40c1-be48-cbe02ca98a3a" />


## Testing Your First Request

To verify your setup is working correctly:

1. Open the **General Services** folder
2. Select the **Get Wallet Balance** request
3. Click **Send**
4. You should receive a successful response with your wallet balance


## Troubleshooting

If you encounter issues with the collection:

1. **Authentication Errors**
   - Verify your OAuth credentials (client ID and secret) are correctly set in the environment
   - Check that your OAuth token hasn't expired (tokens typically expire after a set time)
   - Try requesting a new token if authentication fails

2. **Request Failures**
   - Check the response body for specific error messages
   - Verify all required fields are included in your request
   - Ensure date formats follow YYYY-MM-DD pattern

3. **Postman-specific Issues**
   - Ensure you're using the latest version of Postman
   - Try resetting the environment variables
   - Clear the cookies and cache in Postman settings


