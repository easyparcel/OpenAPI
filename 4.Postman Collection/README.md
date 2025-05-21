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

### Option 1: Import via URL

1. Open Postman
2. Click **Import** in the top-left corner
3. Choose the **Link** tab
4. Enter the collection URL: `https://planetary-resonance-571252.postman.co/workspace/My-Workspace~cd21b7fe-2e31-49a6-8f44-71a2ce36c72c/collection/40226622-aed30dc0-ace2-4531-ad4c-7a050d1fd13e?action=share&creator=40226622`
5. Click **Import**

### Option 2: Import from File

1. Download the collection JSON file from our developer portal
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

### Shipping Flow Example

A typical shipping workflow using this collection:

1. **Get Quotation**
   - Use the "Get Quotation" request in the Order Flow folder
   - Fill in the required parameters for your shipment
   - Send the request to get available shipping options

2. **Submit Order**
   - Use the "Submit Order" request
   - Update the request body with your shipment details
   - Include the `service_id` from the quotation response
   - Send the request to create the shipment

3. **View Shipment Details**
   - Use the "Get Shipment Details" request
   - Enter the `shipment_number` from the submit order response
   - Send the request to view the shipment status

### Ondemand Delivery Example

1. **Get Ondemand Quotation**
   - Use the "Get Ondemand Quotation" request
   - Provide pickup and delivery details
   - Send the request to get available options

2. **Submit Ondemand Order**
   - Use the "Submit Ondemand Order" request
   - Include the details and pricing from the quotation
   - Send the request to create the booking

## Request and Response Examples

### Example: Get Quotation

Request:
```json
{
  "shipment": [
    {
      "sender": {
        "postcode": "10150",
        "subdivison_code": "MY-02",
        "country": "MY"
      },
      "receiver": {
        "postcode": "018916",
        "subdivison_code": "SG-04",
        "country": "SG"
      },
      "parcel_value": 50,
      "weight": 0.5,
      "width": 5,
      "length": 5,
      "height": 5
    }
  ]
}
```

### Example: Submit Order

Request:
```json
{
  "shipment": [
    {
      "service_id": "EP-CS09Q",
      "collection_date": "2025-05-02",
      "weight": 2.5,
      "height": 30,
      "length": 40,
      "width": 20,
      "item": [
        {
          "content": "Electronics",
          "weight": 0.5,
          "height": 30,
          "length": 40,
          "width": 20,
          "currency_code": "MYR",
          "value": 500,
          "quantity": 1
        }
      ],
      "sender": {
        "name": "John Doe",
        "company": "ABC Corp",
        "phone_number_country_code": "+60",
        "phone_number": "1163642281",
        "email": "test@easyparcel.com",
        "address_1": "123 Main St",
        "address_2": "Apt 4B",
        "postcode": "10150",
        "city": "Lunas",
        "subdivison_code": "MY-07",
        "country_code": "MY"
      },
      "receiver": {
        "name": "Jane Smith",
        "company": "XYZ Inc",
        "phone_number_country_code": "+60",
        "phone_number": "1163642281",
        "email": "test@easyparcel.com",
        "address_1": "456 High St",
        "address_2": "Floor 2",
        "postcode": "11950",
        "city": "Bayan Lepas",
        "subdivison_code": "MY-07",
        "country_code": "MY"
      },
      "feature": {
        "sms_tracking": true,
        "email_tracking": true,
        "whatsapp_tracking": false,
        "awb_branding": false
      }
    }
  ]
}
```

## Pre-request Scripts

Some requests in the collection use pre-request scripts to:

1. Generate timestamps and dates
2. Format request data
3. Set dynamic variables

You can view and modify these scripts by selecting a request and clicking on the "Pre-request Script" tab.

## Working with Environments

The collection supports multiple environments to easily switch between:

1. **Development** - For testing during implementation
2. **Production** - For live API interactions

To switch environments:
1. Select the environment dropdown in the top-right corner of Postman
2. Choose the desired environment

## Collection Variables

The collection includes the following built-in variables:

| Variable Name | Description |
|---------------|-------------|
| `currentDate` | Automatically set to today's date |
| `lastShipmentNumber` | Stores the most recent shipment number |
| `lastResponseBody` | Stores the last API response for reference |

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
[![Previous Section←](https://img.shields.io/badge/Previous_Section_%E2%86%90-FF7733?style=for-the-badge&scale=1.3)](../3.OAuth%20Authentication/1.%20oauth%20authentication%20guide.md)
[![Next Section →](https://img.shields.io/badge/Next_Section_%E2%86%92-00CC88?style=for-the-badge&scale=1.3)](../5.API%20endpoint/README.md)

</div>
