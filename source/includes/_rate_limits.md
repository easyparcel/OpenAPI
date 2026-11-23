<h1 id="rate-limits"><span style="color: black;">Rate limits</span></h1>

The EasyParcel Open API limits how much each shipping account can use each endpoint. This keeps the API fast and fair for everyone. If your integration follows this section, it should never be refused.

<h2 id="rate-limits-short-version">The short version</h2>

- Limits are **per shipping account, per endpoint**. Every app and API key on the same account shares them.
- **Shipment quotations are counted by shipment.** One quotation request with 10 shipments uses 10.
- **Every other endpoint is counted by request.** Each request uses 1, however many items it carries.
- Your allowance **refills gradually**. It doesn't wait for the next minute to start.
- Over a limit, you get **HTTP 429**. Wait the number of seconds in the `Retry-After` header, then try again.
- Every response tells you how much you have left, in the `RateLimit` and `X-RateLimit-*` headers.

<h2 id="rate-limits-words">Words used in this section</h2>

| Word | Meaning |
|---|---|
| **Shipping account** | The EasyParcel account your access token works on. It has its own wallet and shipments. Limits are counted per shipping account. |
| **Login** | One person's EasyParcel sign-in. One login can work on several shipping accounts, for example an agency with many clients. |
| **Allowance** | How many you can still send on one endpoint right now. |
| **Per minute** | How fast your allowance refills. |
| **Max at once** | The most your allowance can hold: how many you can send back to back after a quiet moment. |
| **Per day** | A daily cap. Only some endpoints have one, and only for some accounts. |

<h2 id="rate-limits-counting">How requests are counted</h2>

<h3 id="rate-limits-by-shipment">Shipment quotations: by shipment</h3>

`/shipment/quotations` is the only endpoint counted by shipment. Each shipment in the request's `shipment` list (`list` on the unversioned 2025-03 path) uses 1.

| You send | It uses |
|---|---|
| 1 quotation request with 1 shipment | 1 |
| 1 quotation request with 10 shipments | 10 |
| 1 quotation request with 50 shipments (the most one request can carry) | 50 |
| 5 quotation requests with 10 shipments each | 50 |

So the Live limit of **120 a minute** on Shipment quotations means **120 shipments a minute**, not 120 requests. One request of 50 shipments and 50 requests of 1 shipment use the same allowance.

What counts is the shipments you send, not the rates you get back. A shipment that returns rates from 15 couriers still uses 1.

The same goes for Shipment quotations' per-day limit and combined limit per login: *100 a day* means 100 shipments a day.

<h3 id="rate-limits-by-request">Every other endpoint: by request</h3>

Every other endpoint uses 1 per request, however many items the request carries.

| You send | It uses |
|---|---|
| 1 Submit orders request with 200 shipments | 1 |
| 1 Shipment cancel request with 50 shipments | 1 |
| 1 Insurance quotation request with 50 items | 1 |
| 1 Tracking status request | 1 |

Some of these endpoints take a list and have a **most items per request** (see [Limits](#rate-limits-table)). That is a size cap on one request, not a counting unit.

<h3 id="rate-limits-what-counts">What uses your allowance</h3>

| What happens to the request | Uses your allowance? |
|---|---|
| It goes through | Yes |
| It passes the limit check, then the endpoint rejects it (for example, a required field is missing) | **Yes** |
| It is refused by a limit (HTTP 429) | No |
| It carries too many items (HTTP 400 `BATCH_TOO_LARGE`) | No |
| It fails authentication | No |

A request the endpoint rejects still counts, so check your input before you send it.

<h2 id="rate-limits-refill">How your allowance refills</h2>

Think of each endpoint's allowance as a bucket:

- The bucket holds **Max at once**, and starts full.
- Each request takes 1 out, or 1 per shipment for Shipment quotations.
- It refills at the **per-minute** rate, a little at a time. 120 a minute means 1 comes back every half second.
- A request that needs more than is in the bucket is refused as a whole. Nothing in it is processed, and nothing is taken out.

**Max at once** is the same as the per-minute number, with one exception. Shipment quotations on a Not topped up account allow 10 a minute and 50 at once, so a full 50-shipment quotation always fits after a quiet moment.

**Per day** counts up from 0 and starts again at 00:00 Malaysia time (UTC+8, which is 16:00 UTC). It doesn't refill during the day.

<h3 id="rate-limits-example-live">Example: Shipment quotations on a Live account</h3>

120 shipments a minute, 120 at once. 2 shipments come back each second.

| Time | You send | Left in the bucket | Result |
|---|---|---|---|
| 0 s | 50 shipments | 70 | Allowed |
| 0 s | 50 shipments | 20 | Allowed |
| 2 s | 50 shipments | 24 (4 came back) | **Refused, HTTP 429.** It needs 50 and only 24 are left. `Retry-After: 13`, the time for 26 more to come back. |
| 15 s | 50 shipments | 0 | Allowed |

To quote many shipments at a steady pace on Live, send one 50-shipment request every 25 seconds.

<h3 id="rate-limits-example-not-topped-up">Example: Shipment quotations on a Not topped up account</h3>

10 shipments a minute, 50 at once, 100 a day.

- It can send one 50-shipment quotation straight away.
- After that, 1 shipment comes back every 6 seconds, so the next 50-shipment quotation fits 5 minutes later.
- Once it has quoted 100 shipments in a day, quotations are refused until 00:00 Malaysia time.

<h2 id="rate-limits-which-apply">Which limits apply to your account</h2>

| Your account | Limits used |
|---|---|
| A live account that has topped up its wallet at least once | **Live** |
| A live account that has never topped up | **Not topped up**: the same as Live, except the quotation endpoints, which are lower and have a per-day limit. Your first top-up moves the account to Live within about 30 seconds. |
| A sandbox (test) account | **Sandbox** |

<h3 id="rate-limits-combined-per-login">Combined limit per login</h3>

On the quotation endpoints, one login's live accounts also share a **combined limit per login**.

For example, an agency login works on 5 live accounts. Each account can quote 120 shipments a minute on its own, but together the 5 can quote at most 240 shipments a minute.

- It applies only to the quotation endpoints, the ones with a number in the *Combined limit per login* column.
- Each account's own limit still applies too. Whichever limit is reached first refuses the request.
- Live and Not topped up accounts count towards it. Sandbox accounts don't.
- It is counted the same way as the endpoint: by shipment for Shipment quotations, by request for the others.

<h2 id="rate-limits-table">Limits</h2>

Paths are shown without the `/open_api/<version>` prefix. Every version of an endpoint (`/open_api/2025-12/shipment/quotations`, `/open_api/2026-09/shipment/quotations` and so on) shares one allowance.

<h3 id="rate-limits-quotation-endpoints">Quotation endpoints</h3>

These limits depend on which limits your account uses.

| Endpoint | Path | Live | Not topped up | Sandbox | Combined limit per login | Most items per request |
|---|---|---|---|---|---|---|
| Shipment quotations | `/shipment/quotations` | 120 **shipments** / min | 10 **shipments** / min (50 at once)<br>100 **shipments** / day | 60 **shipments** / min | 240 **shipments** / min | 50 shipments |
| On-demand quotation | `/ondemand/quotation` | 20 requests / min | 10 requests / min<br>100 requests / day | 20 requests / min | 40 requests / min | — |
| Insurance quotation | `/insurance_quotations`<br>`/shipment/insurance_quotations` | 60 requests / min | 10 requests / min<br>100 requests / day | 60 requests / min | 120 requests / min | 50 items |
| Shipment coupon list | `/shipment/get_coupon_list` | 60 requests / min | 10 requests / min<br>100 requests / day | 60 requests / min | 120 requests / min | — |
| On-demand coupon list | `/ondemand/get_coupon_list` | 30 requests / min | 10 requests / min<br>100 requests / day | 30 requests / min | 60 requests / min | — |

<h3 id="rate-limits-other-endpoints">All other endpoints</h3>

These are counted by request and are the same for Live, Not topped up and Sandbox accounts. They have no per-day limit and no combined limit per login.

| Endpoint | Path | Requests per minute | Most items per request |
|---|---|---|---|
| Submit orders | `/shipment/submit_orders` | 2,000 | 200 shipments |
| On-demand order | `/ondemand/order` | 100 | — |
| Shipment cancel | `/shipment/cancel` | 60 | 50 shipments |
| On-demand cancel | `/ondemand/cancel` | 60 | — |
| Tracking status | `/shipment/tracking_status` | 120 | 50 AWBs |
| Shipment list | `/shipment/list` | 60 | — |
| Shipment details | `/shipment/details` | 300 | — |
| On-demand list | `/ondemand/list` | 60 | — |
| On-demand details | `/ondemand/details` | 300 | — |
| Courier list | `/courier/list` | 120 | — |
| Drop-off points | `/courier/get_courier_dropoff_points`<br>`/shipment/get_courier_dropoff_points` | 120 | — |
| Parcel categories | `/parcel_category/list` | 120 | — |
| HS codes | `/hscode/list` | 120 | — |
| Wallet | `/wallet` | 120 | — |
| Account information | `/account/get_account_information` | 120 | — |
| Malaysia e-invoice submit | `/einvoice/malaysia/submit` | 120 | 100 invoices |
| Malaysia e-invoice verify access | `/einvoice/malaysia/verify_access` | 120 | — |

**Need more?** If your integration genuinely needs a higher limit, contact EasyParcel support with your account ID and the endpoint. Limits can be raised for a single account.

<h2 id="rate-limits-headers">Reading the response headers</h2>

Every response from a limited endpoint tells you where you stand. This is a 3-shipment quotation on a Live account:

```http
HTTP/1.1 200 OK
RateLimit-Policy: "minute";q=120;w=60, "login_minute";q=240;w=60
RateLimit: "minute";r=117;t=2, "login_minute";r=237;t=1
X-RateLimit-Limit: 120
X-RateLimit-Remaining: 117
X-RateLimit-Reset: 1792750377
```

In words: this account can quote 117 more shipments right now, and its allowance is full again in 2 seconds. Across all the accounts of this login, 237 more shipments can be quoted.

| Header | Meaning |
|---|---|
| `RateLimit-Policy` | Each limit that applies: its name, `q` the per-minute or per-day number, `w` the window in seconds. The names are `minute` (per minute), `day` (per day) and `login_minute` (the combined limit per login). |
| `RateLimit` | For each limit: `r` how many you can send right now, `t` seconds until it is full again (per minute) or starts again (per day). |
| `X-RateLimit-Limit` | For the limit closest to running out: its Max at once, or its per-day number for a per-day limit. |
| `X-RateLimit-Remaining` | How many you can send right now on that limit. |
| `X-RateLimit-Reset` | When that limit is full again or starts again, as a Unix time in seconds. |

Things that can look odd:

- **`Remaining` didn't go down.** Per minute refills gradually, so what one request used may have come back before the next. A per-day limit doesn't refill, so its `r` only goes down.
- **`r` is higher than `q`.** `q` is the per-minute number, while `r` counts down from Max at once. On a Not topped up account, Shipment quotations allow 10 a minute and 50 at once, so after a 3-shipment quotation you see `q=10` and `r=47`, with `X-RateLimit-Limit: 50`.

`RateLimit-Policy` and `RateLimit` follow the IETF draft *RateLimit header fields for HTTP*. Endpoints that aren't limited send none of these headers.

<h2 id="rate-limits-429">When a limit is reached: HTTP 429</h2>

This is the refused request from the [Live example](#rate-limits-example-live): the third 50-shipment quotation in 2 seconds.

```http
HTTP/1.1 429 Too Many Requests
Retry-After: 13
RateLimit-Policy: "minute";q=120;w=60, "login_minute";q=240;w=60
RateLimit: "minute";r=24;t=48, "login_minute";r=148;t=23
X-RateLimit-Limit: 120
X-RateLimit-Remaining: 24
X-RateLimit-Reset: 1792750425
```

```json
{
  "status_code": 429,
  "request_id": "1792750377412.3f2b8c1e-7d4a-4f6b-9a0e-5c1d2e3f4a5b",
  "code": "RATE_LIMITED",
  "message": "Rate limit reached for Shipment quotations on this account: 120 per minute. Retry in 13 seconds.",
  "data": null,
  "errors": [
    {
      "code": "RATE_LIMITED",
      "message": "Rate limit reached for Shipment quotations on this account: 120 per minute. Retry in 13 seconds."
    }
  ],
  "rate_limit": {
    "policy": "minute",
    "limit": 120,
    "remaining": 24,
    "reset": 48,
    "retry_after": 13,
    "limit_set": "live"
  }
}
```

Nothing in a refused request is processed. `Retry-After` is how long until the **whole** request fits. A smaller request may fit sooner: here, a quotation of up to 24 shipments would go through straight away.

| Field | Meaning |
|---|---|
| `code` | `RATE_LIMITED` when a limit is reached. `ENDPOINT_BLOCKED` when EasyParcel has blocked this endpoint for your account, or blocked quotations for your login. |
| `rate_limit.policy` | Which limit was reached: `minute` (per minute), `day` (per day), `login_minute` (the combined limit per login), `blocked` (this endpoint is blocked for your account) or `login_blocked` (quotations are blocked for your login on all its accounts). |
| `rate_limit.limit` | The limit's per-minute or per-day number, as in the message. `null` for a block. |
| `rate_limit.remaining` | How many you can send right now on that limit. |
| `rate_limit.reset` | Seconds until that limit is full again or starts again. `null` for a block. |
| `rate_limit.retry_after` | Seconds to wait before trying again. The same as the `Retry-After` header. |
| `rate_limit.limit_set` | Which limits the account uses: `live` (Live), `not_topped_up` (Not topped up) or `sandbox` (Sandbox). |

The message says which limit was reached:

| Message | What to do |
|---|---|
| *Rate limit reached for Shipment quotations on this account: 120 per minute. Retry in 13 seconds.* | Wait `Retry-After` seconds. |
| *Rate limit reached for Shipment quotations across the accounts of this login: 240 per minute. Retry in 3 seconds.* | The combined limit per login. Wait `Retry-After` seconds. |
| *Daily limit reached for Shipment quotations on this account: 100 per day. It resets at 00:00 Malaysia time. Top up your wallet to raise this limit.* | Wait until 00:00 Malaysia time, or top up. |
| *Shipment quotations is blocked for this account. Contact EasyParcel support.* | `ENDPOINT_BLOCKED`. Retrying won't help: contact support. `Retry-After` is 3600. |
| *Shipment quotations is blocked for this login on all its accounts. Contact EasyParcel support.* | `ENDPOINT_BLOCKED`. Retrying won't help: contact support. `Retry-After` is 3600. |

On a Not topped up account, the message ends with *Top up your wallet to raise this limit.* whenever topping up would raise the limit that was reached.

A blocked request carries only the `Retry-After` header, not the other rate-limit headers.

<h2 id="rate-limits-batch-too-large">Too many items in one request: HTTP 400</h2>

Some endpoints take a list. The *Most items per request* column in [Limits](#rate-limits-table) shows the most each request can carry. A larger request is refused before anything is processed, and uses none of your allowance:

```json
{
  "status_code": 400,
  "request_id": "1792750377412.3f2b8c1e-7d4a-4f6b-9a0e-5c1d2e3f4a5b",
  "code": "BATCH_TOO_LARGE",
  "message": "Too many items in one request: Shipment quotations takes at most 50 shipments per request, and this one has 51.",
  "data": null,
  "errors": [
    {
      "code": "BATCH_TOO_LARGE",
      "message": "Too many items in one request: Shipment quotations takes at most 50 shipments per request, and this one has 51."
    }
  ],
  "batch": { "cap": 50, "size": 51 }
}
```

Split the list into several requests. Sending the same request again won't help.

<h2 id="rate-limits-handling">Handling limits well</h2>

1. **On a 429, wait `Retry-After` seconds, then try again.** Don't retry straight away: the retry will be refused too.
2. **Don't retry `ENDPOINT_BLOCKED`.** Contact EasyParcel support instead.
3. **Watch `RateLimit` or `X-RateLimit-Remaining`.** Slow down before it reaches 0, instead of waiting for a 429.
4. **Send at a steady pace.** A queue that sends steadily stays under every per-minute limit. A loop that sends everything at once empties the bucket, then has to wait.
5. **Count shipments, not requests, for Shipment quotations.** Batching shipments into fewer requests doesn't save allowance. It only saves round trips.
6. **When there's no `Retry-After`** (for example, a network error), retry with growing waits: 1, 2, 4, then 8 seconds, plus a random fraction of a second. Stop after a few tries.
7. **Keep reference data.** The courier list, parcel categories and HS codes rarely change. Fetch them once a day, not before every quotation.
8. **Quote what you'll ship.** Quote when a customer checks out or a merchant books, not ahead of time for every possible route.
9. **Don't share one account across unrelated merchants.** Each merchant should connect their own EasyParcel account.

A simple retry, in JavaScript:

```js
// Sends again after a 429, waiting as long as Retry-After says.
async function sendWithRetry(send, maxTries = 3) {
  for (let attempt = 1; ; attempt++) {
    const res = await send();
    if (res.status !== 429 || attempt === maxTries) return res;
    const body = await res.clone().json();
    if (body.code === 'ENDPOINT_BLOCKED') return res; // retrying won't help
    const seconds = Number(res.headers.get('Retry-After')) || 1;
    await new Promise((resolve) => setTimeout(resolve, seconds * 1000));
  }
}
```

<h2 id="rate-limits-sandbox">Sandbox</h2>

- Sandbox accounts use the limits in the **Sandbox** column, so a test suite behaves the same from run to run.
- **Sandbox prices are for testing only. They are not live prices.** They differ from what a live account is charged, so never show sandbox prices to customers or use them to set your own prices. Use a live account to check real prices.
- A sandbox booking is charged exactly the sandbox price you were quoted, so end-to-end tests can compare the two.

<h2 id="rate-limits-faq">Common questions</h2>

**My quotation request used 10 of my allowance, not 1. Why?**
It had 10 shipments. Shipment quotations are counted by shipment. Every other endpoint is counted by request.

**Does each API key or app get its own allowance?**
No. Every app and API key on the same shipping account shares one allowance per endpoint.

**Does calling a different API version give me more?**
No. Every version of an endpoint shares one allowance.

**Is a refused request counted?**
No. A 429, or a 400 for too many items, uses nothing. A request the endpoint itself rejects, for example because a field is missing, does count.

**When does the daily limit start again?**
At 00:00 Malaysia time, which is 16:00 UTC.

**I just topped up. When do I get Live limits?**
Within about 30 seconds of your first top-up.
