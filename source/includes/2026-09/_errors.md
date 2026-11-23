<h1 id="errors-2026-09">Errors</h1>

The EasyParcel Open API uses standard HTTP status codes. Responses carry the same code in the `status_code` field of the JSON body, together with a `request_id`. Include the `request_id` when you contact support.

```json
{
    "status_code": 400,
    "request_id": "1769761472947.b7a9d539-083a-48d7-8974-0fd6f13baa72",
    "message": "Missing Required Param",
    "data": {
        "awb_numbers": ["The awb numbers field is required."]
    }
}
```

Status Code | Meaning | What to do
----------- | ------- | ----------
200 | Success. Batch endpoints (quotations, submit orders, cancel, tracking status, insurance quotations) also return 200 when some or all items fail. | Check each item's `status` and `errors` / `message`.
400 | Bad Request. A required field is missing or invalid, or the request carries too many items (`BATCH_TOO_LARGE`). | Fix the request using `message` and `data`. Don't retry unchanged.
401 | Unauthorized. The access token is missing, invalid or expired. | Refresh the access token, or ask the user to reconnect the app.
403 | Forbidden. The token can't be used for this request. For example, the phone number of the user who connected the app is not verified (`PHONE_NUMBER_UNVERIFIED`), or the refresh token is no longer valid. | Follow the message. Retrying won't help until it's fixed.
404 | Not Found. The shipment or order doesn't exist in this account. | Check the number and the account the token belongs to.
429 | Too Many Requests. A rate limit was reached (`RATE_LIMITED`), or the endpoint is blocked for the account (`ENDPOINT_BLOCKED`). | Wait for `Retry-After` seconds. See [Rate limits](#rate-limits).
500 | Internal Server Error. | Retry later with backoff. If it continues, contact support with the `request_id`.
503 | Service Unavailable. A dependency is temporarily unavailable. | Retry later with backoff.

For the message catalogue, batch-error patterns and handling tips, see the [EasyParcel API Error Handling Guide](#reference-easyparcel-api-error-handling-guide-2026-09).
