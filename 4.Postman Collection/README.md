# EasyParcel API Postman Collection Guide

This guide helps you get started with the EasyParcel API using Postman, providing instructions for importing, configuring, and using our Postman collection.

## Getting Started

Our Postman collection provides a convenient way to explore and test the EasyParcel API endpoints. Follow these steps to get up and running quickly.

## Collection Overview

The EasyParcel API Postman collection is organized into the following main folders:

1. **Shipping Services**
   - **Order Flow** - Get quotations, insurance quotes, and submit orders
   - **Listing Flow** - Retrieve and view shipment details
   - **Cancel Orders** - Cancel existing shipments

2. **Ondemand Services**
   - **Ondemand Order Flow** - Get quotations and create on-demand deliveries

3. **General Services**
   - **Courier Listing** - View available couriers
   - **Credit Wallet** - Check your account balance

## Importing the Collection
1. Download the collection JSON file from over here : 
2. Open Postman
3. Click **Import** in the top-left corner
4. Choose the **File** tab and select the downloaded JSON file
5. Click **Import**

## Configuration

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
   - **Grant Type**: Client Credentials
   - **Access Token URL**: https://api.easyparcel.com/oauth/token
   - **Client ID**: Your EasyParcel client ID
   - **Client Secret**: Your EasyParcel client secret
   - **Scope**: (leave as is or use specific scopes if provided)
4. Click **Request Token**
5. Once you receive the token, click **Use Token**

The collection will automatically include the token in all requests.

## Testing Your First Request

To verify your setup is working correctly:

1. Open the **General Services** folder
2. Select the **Get Wallet Balance** request
3. Click **Send**
4. You should receive a successful response with your wallet balance

## Using the Collection



## Pagination

For listing endpoints that return multiple records, the collection includes helpers for pagination:

1. Use the "Get Shipment List" or "Get Ondemand List" requests
2. The response will include shipments/bookings
3. To get the next page:
   - Note the last item's shipment_number/booking_number
   - Update the "before_shipment_number" or "before_booking_number" parameter
   - Send the request again

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

## Getting Help

If you need assistance with the EasyParcel API or this Postman collection:

- Visit our [API Documentation](https://developer.easyparcel.com)
- Email our developer support at api@easyparcel.com
- Check the [Error Handling Guide](../7.References/7.error%20handling.md) for common issues

## Contributing

We welcome feedback and suggestions to improve this collection. Please contact our developer support team with your ideas or issues.

---
<div align="center" style="margin:2rem 0">

[![Back to Docs](https://img.shields.io/badge/Back_to_Docs-00AAEE?style=for-the-badge&scale=1.3)](../README.md)
[![Previous Section←](https://img.shields.io/badge/Previous_Section_%E2%86%90-FF7733?style=for-the-badge&scale=1.3)](../3.OAuth%20Authentication)
[![1.How_to_import_json_file_to_Postman →](https://img.shields.io/badge/1.How_to_import_json_file_to_Postman_%E2%86%92-00CC88?style=for-the-badge&scale=1.3)](../4.Postman%20Collection/1.Step%20On%20How%20to%20import%20json%20file%20in%20Postman.md)
[![Next Section →](https://img.shields.io/badge/Next_Section_%E2%86%92-00CC88?style=for-the-badge&scale=1.3)](../5.API%20endpoint/README.md)

</div>
