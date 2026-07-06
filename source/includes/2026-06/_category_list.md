<h1 id="category-list-2026-06">Parcel Category List</h1>

This endpoint allows users to retrieve a list of available parcel categories.

<h2 id="http-request-category-list-2026-06">HTTP Request (Parcel Category List)</h2>

`GET https://api.easyparcel.com/open_api/2026-06/parcel_category/list`

<h2 id="returned-category-list-2026-06">Parcel Category Response</h2>

### Response Sample

```json
{
    "status_code": 200,
    "request_id": "1783306464627.6926767a-2142-4181-ae1c-887975bf8dec",
    "message": "Success",
    "data": [
        {
            "id": 1,
            "name": "Bags & Luggages"
        },
        {
            "id": 2,
            "name": "Board Games"
        },
        {
            "id": 3,
            "name": "Computers & Laptops"
        },
        {
            "id": 4,
            "name": "Cameras"
        },
        {
            "id": 5,
            "name": "Books"
        },
        {
            "id": 6,
            "name": "Dry Food"
        },
        {
            "id": 7,
            "name": "Fashion"
        },
        {
            "id": 8,
            "name": "Fashion Accessories"
        },
        {
            "id": 9,
            "name": "Gaming"
        },
        {
            "id": 10,
            "name": "Health & Beauty"
        },
        {
            "id": 11,
            "name": "Home Appliances"
        },
        {
            "id": 12,
            "name": "Home Decor"
        },
        {
            "id": 13,
            "name": "Jewelry"
        },
        {
            "id": 14,
            "name": "Mobile Phones"
        },
        {
            "id": 15,
            "name": "Pet Accessory"
        },
        {
            "id": 16,
            "name": "Supplements"
        },
        {
            "id": 17,
            "name": "Sport & Leisure"
        },
        {
            "id": 18,
            "name": "Tablets"
        },
        {
            "id": 19,
            "name": "Toys"
        },
        {
            "id": 20,
            "name": "Watches"
        },
    ]
}
```

### Main Response Structure

| Parameter    | Type    | Description                           |
|--------------|---------|---------------------------------------|
| status_code  | int     | Status code of the response           |
| request_id   | string  | Unique request identifier             |
| message      | string  | Response message                      |
| data         | array   | A list of parcel categories            |

### Category Object

| Parameter    | Type    | Description                           |
|--------------|---------|---------------------------------------|
| id           | int     | Unique category ID                    |
| name         | string  | Name of parcel category               |


### Common Status Codes

| Status Code  | Description       | 
|--------------|-------------------|
| 200          | Successful request| 
| 400          | Bad request       | 
| 401          | Unauthorized      | 
| 500          | Server error      | 

<h2 id="usage-notes-category-2026-06">Usage Notes (Category List)</h2>

1. This endpoint does not require any request parameters.
2. The id returned is used in shipment quotation.
3. Always use the latest response to ensure correct classification.

