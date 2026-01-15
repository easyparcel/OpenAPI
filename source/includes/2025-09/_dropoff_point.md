# Courier Drop-off Points Feature

The courier drop-off points feature allows customers to retrieve a list of available drop-off locations where they can physically bring their parcels for shipment. This helps users find convenient locations near them to drop off their packages instead of scheduling a pickup.


## Retrieving Drop-off Points

Customers can retrieve a list of available drop-off locations for a specific courier using the following endpoint:

### HTTP Request (Drop-off Points)

`POST https://api.easyparcel.com/open_api/2025-09/courier/get_courier_dropoff_points`

This endpoint returns detailed information about drop-off locations including addresses, operating hours, and contact information based on the specified courier and location parameters.


## Drop-off Points Request

### Submitting Location Details to Get Available Drop-off Points

You can query drop-off points by providing courier and location information to find the nearest available locations.

### Sample Drop-off Points Request:

```json
{
    "courier_id": "EP-CR0A",
    "country_code": "MY",
    "postcode": "09600",
    "city": "Lunas",
    "state_code": "MY-02"
}
```

### Request Parameters

| Parameter    | Type   | Required | Description                                                    |
|--------------|--------|----------|----------------------------------------------------------------|
| courier_id   | string | Yes      | EasyParcel courier service ID (e.g., "EP-CR0A")               |
| country_code | string | Yes      | Country code (ISO 3166-1 alpha-2, e.g., "MY")                 |
| postcode     | string | Yes      | Postcode/ZIP code of the search location                       |
| city         | string | Yes      | City name for the search location                              |
| state_code   | string | Yes      | State/subdivision code (ISO 3166-2 format, e.g., "MY-02")     |


## Drop-off Points Response

### 🏢 Drop-off Points API - Response Parameters

### Sample Response for Drop-off Points

```json
{
    "status_code": 200,
    "request_id": "1762740567664.ba412296-e538-49ad-99f0-78e694bde618",
    "message": "Success",
    "data": [
        {
            "point_id": "EP-CB0FF",
            "name": "Pejabat Pos Besar Pulau Pinang",
            "address_1": "Tingkat Bawah, Bangunan Tuanku Syed Putra",
            "address_2": "Leboh Downing",
            "address_3": "",
            "address_4": "",
            "postcode": "10670",
            "city": "Pulau Pinang",
            "state": "png",
            "phone_number": "04-2619222",
            "info": "",
            "image": "",
            "start_time": "08:00:00",
            "end_time": "13:00:00"
        },
        {
            "point_id": "EP-CB0F9",
            "name": "Pos Malaysia Ayer Itam",
            "address_1": "JKR 19",
            "address_2": "Jalan Paya Terubung",
            "address_3": "",
            "address_4": "",
            "postcode": "11500",
            "city": "Ayer Itam",
            "state": "png",
            "phone_number": "04-8283226",
            "info": "",
            "image": "",
            "start_time": "08:00:00",
            "end_time": "13:00:00"
        },
        {
            "point_id": "EP-CB0F5",
            "name": "Pos Malaysia Balik Pulau",
            "address_1": "JKR 2312",
            "address_2": "Jalan Besar",
            "address_3": "",
            "address_4": "",
            "postcode": "11000",
            "city": "Balik Pulau",
            "state": "png",
            "phone_number": "04-8668204",
            "info": "",
            "image": "",
            "start_time": "08:00:00",
            "end_time": "13:00:00"
        },
        {
            "point_id": "EP-CB0FG",
            "name": "Pos Malaysia Batu Ferringghi",
            "address_1": "JKR 2340",
            "address_2": "Jalan Batu Ferringghi",
            "address_3": "",
            "address_4": "",
            "postcode": "11100",
            "city": "Batu Ferringghi",
            "state": "png",
            "phone_number": "04-8668204",
            "info": "",
            "image": "",
            "start_time": "08:00:00",
            "end_time": "13:00:00"
        }
    ]
}
```

### Main Response

| Parameter    | Type   | Description                                             |
|--------------|--------|---------------------------------------------------------|
| status_code  | int    | HTTP status code indicating success or failure          |
| request_id   | string | Unique identifier for the API request                   |
| message      | string | Description of the response status                      |
| data         | array  | Array of drop-off point objects                         |

### Drop-off Point Object (Inside `data` array)

| Parameter    | Type   | Description                                                      |
|--------------|--------|------------------------------------------------------------------|
| point_id     | string | Unique identifier for the drop-off point                         |
| name         | string | Name of the drop-off location                                    |
| address_1    | string | Primary address line                                             |
| address_2    | string | Secondary address line (street name, building details)           |
| address_3    | string | Additional address line (may be empty)                           |
| address_4    | string | Additional address line (may be empty)                           |
| postcode     | string | Postcode of the drop-off location                                |
| city         | string | City where the drop-off point is located                         |
| state        | string | State/region code or abbreviation                                |
| phone_number | string | Contact phone number for the drop-off location                   |
| info         | string | Additional information or notes about the location (may be empty) |
| image        | string | URL to an image of the location (may be empty)                   |
| start_time   | string | Opening time in HH:MM:SS format (24-hour)                        |
| end_time     | string | Closing time in HH:MM:SS format (24-hour)                        |


## Understanding Operating Hours

Drop-off points have specific operating hours when customers can drop off their parcels:

- **start_time**: The time when the location opens for drop-offs
- **end_time**: The time when the location closes for drop-offs
- **Format**: Times are provided in 24-hour format (HH:MM:SS)

### Example:
```
start_time: "08:00:00" → Opens at 8:00 AM
end_time: "13:00:00" → Closes at 1:00 PM
```

**Important**: Ensure customers arrive before the closing time to successfully drop off their parcels. Some locations may have limited operating hours (e.g., morning only).

<h2 id="dropoffpoint-usage-notes">Usage Notes</h2>

- **Location-based Search**: Results are typically sorted by proximity to the specified postcode and city.
- **Courier-specific**: Each courier may have different drop-off locations. Always query with the specific courier ID you're using.
- **Operating Hours**: Always check the `start_time` and `end_time` to inform customers of available drop-off windows.
- **Empty Fields**: Some fields like `address_3`, `address_4`, `info`, and `image` may be empty strings if not applicable.
- **Phone Contact**: The `phone_number` can be used to verify operating hours or get additional information about the location.


<h2 id="dropoffpoint-example-use-case">Example Use Cases</h2>

### Finding Drop-off Points in Kuala Lumpur

```json
{
    "courier_id": "EP-CR0A",
    "country_code": "MY",
    "postcode": "50000",
    "city": "Kuala Lumpur",
    "state_code": "MY-14"
}
```

### Finding Drop-off Points in Penang

```json
{
    "courier_id": "EP-CR0A",
    "country_code": "MY",
    "postcode": "10000",
    "city": "George Town",
    "state_code": "MY-07"
}
```

### Different Courier Service

```json
{
    "courier_id": "EP-CR0B",
    "country_code": "MY",
    "postcode": "80000",
    "city": "Johor Bahru",
    "state_code": "MY-01"
}
```


## Displaying Drop-off Points to Customers

When presenting drop-off points to your users, consider displaying:

1. **Location Name** - Clear identification of the drop-off point
2. **Full Address** - Concatenate address lines for easy navigation
3. **Operating Hours** - Display in user-friendly format (e.g., "8:00 AM - 1:00 PM")
4. **Distance** - Calculate and show distance from user's location (if possible)
5. **Contact Number** - Allow users to call for inquiries
6. **Map Integration** - Use address/postcode to show location on a map

### Display Example:

```
📍 Pejabat Pos Besar Pulau Pinang
   Tingkat Bawah, Bangunan Tuanku Syed Putra
   Leboh Downing, 10670 Pulau Pinang
   
   ⏰ Operating Hours: 8:00 AM - 1:00 PM
   📞 Phone: 04-2619222
```


## Applying Drop-off Points to Shipments

Once a customer selects a drop-off point, you can include the `point_id` in your shipment submission request to indicate the parcel will be dropped off at that location instead of being picked up.

### Example Drop-off Point Application in Shipment Submission:

```json
{
  "shipment": [
    {
      "service_id": "EP-CS05M",
      "dropoff_point_id": "EP-CB0FF",
      "collection_method": "dropoff",
      // ... other shipment details
    }
  ]
}
```

*Note: Specific implementation may vary based on the shipment submission endpoint requirements.*


<h2 id="dropoffpoint-error-handling">Error Handling</h2>

### No Drop-off Points Available

If no drop-off points are found for the specified location:

```json
{
    "status_code": 200,
    "request_id": "1762740567664.xyz-123-abc",
    "message": "No drop-off points found",
    "data": []
}
```

### Invalid Courier or Location

If the courier ID is invalid or doesn't service the specified location:

```json
{
    "status_code": 400,
    "request_id": "1762740567664.xyz-123-abc",
    "message": "Invalid courier ID or location not serviced",
    "data": null
}
```


## State Codes Reference (Malaysia)

Common Malaysian state codes (ISO 3166-2):

| State Code | State Name              |
|------------|-------------------------|
| MY-01      | Johor                   |
| MY-02      | Kedah                   |
| MY-03      | Kelantan                |
| MY-04      | Malacca (Melaka)        |
| MY-05      | Negeri Sembilan         |
| MY-06      | Pahang                  |
| MY-07      | Penang (Pulau Pinang)   |
| MY-08      | Perak                   |
| MY-09      | Perlis                  |
| MY-10      | Selangor                |
| MY-11      | Terengganu              |
| MY-12      | Sabah                   |
| MY-13      | Sarawak                 |
| MY-14      | Kuala Lumpur            |
| MY-15      | Labuan                  |
| MY-16      | Putrajaya               |


## Best Practices

1. **Cache Results**: Consider caching drop-off point data for a reasonable period (e.g., 24 hours) as locations rarely change frequently.
2. **Sort by Distance**: If possible, calculate distance from user's location and sort results accordingly for better UX.
3. **Show Operating Hours Prominently**: Make sure users are aware of the operating hours before traveling to a drop-off point.
4. **Provide Alternatives**: If the nearest drop-off point is far, consider offering pickup service as an alternative.
5. **Verify Before Departure**: Suggest users call the drop-off location to confirm operating hours, especially on public holidays.
6. **Map Integration**: Integrate with mapping services (Google Maps, Waze) to provide navigation directions.
7. **Filter by Time**: Allow users to filter drop-off points based on current time and whether they're currently open.

