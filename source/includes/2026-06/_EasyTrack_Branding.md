<h1 id="EasyTrackBranding-2026-06">EasyTrack Branding </h1>
This is a paid add-on that replaces the default EasyParcel tracking page shown to the receiver with a merchant-branded tracking page (logo, banner, products, etc.), built from an <b>EasyTrack Branding template</b> configured on the EasyParcel Portal.<br><br>

- Enablement is driven by the ```account-level flag account.is_easytrack_branding_enabled``` (configured on the Portal — **not settable via this API**). When on, the account's **default template** (```is_default = 1```) is automatically applied.
- Every request can **override** this per shipment via ```feature.easytrack_branding.enable``` (and optionally choose a **specific** template with ```feature.easytrack_branding.template_id```).
- If the account has **no** EasyTrack Branding template at all, the feature is silently skipped — orders still submit normally, without branding and without charge.
- Template ids are exposed **encoded**, using the same scheme as ```service_id```/```courier_id```, with prefix **```EP-ETBT```** (e.g. ```EP-ETBTA5```). Always echo back the value returned by the quotation endpoint; do not construct or guess this string.


<h2 id="shipment-quotation-EasyTrackBranding-2026-06">Shipment Quotations - EasyTrackBranding </h2>

### Endpoint
```
1.  POST /trunk/shipment/quotations
```
### Authentication
OAuth 2.0 with scopes: ``` account:read ```, ``` wallet:read ```

### Request Example:
```
1. {"shipment": [{"sender":   { "country": "MY", "postcode": "50000", "subdivision_code": "KUL" },"receiver": { "country": "MY", "postcode": "10000", "subdivision_code": "PNG" },"weight": 1,"width": 10,"length": 10,"height": 10,"parcel_category_id": 2,"parcel_value": 100}]}

```

#### Request Fields
Parameter | Type | Required | Description | Example
--------- | ---- | -------- | ------------|---------
shipment[].feature.easytrack_branding.enable |boolean/numeric| No | Per-shipment override. Omit to use the account default (**is_easytrack_branding_enabled**). Set **true/1** to force on, **false/0** to force off. | TRUE

#### How It Works
1. The account's ```is_easytrack_branding_enabled``` flag and <b>every</b> EasyTrack Branding template belonging to the account are loaded once per request.
2. Each template is priced individually: base price (``` easytrack_branding_pricing.easytrack_branding_price ```) plus ``` remove_ep_branding_price ``` when that specific template has ``` remove_ep_branding = 1 ```, minus any active account discount (``` account_discount_easytrack_branding```), plus tax (``` EASYTRACK_BRANDING ``` revenue stream).
3. Templates are ordered ``` is_default DESC, id ASC ``` — the <b>first</b> one is the template that will be <b> auto-applied at submit </b> if no ``` template_id ``` override is given.
4. ``` enabled ```reflects the effective state for this shipment (per-request override, else the account flag). Only when ``` enabled = true ``` is the applied template's price + tax folded into ``` pricing.total_amount ``` /  ```pricing.total_features_price ```/ ```pricing.total_features_tax.```
5. ```available_template``` always lists <b>every</b> template on the account (so the caller can pick one), regardless of whether the feature is enabled.

### Response Example — account enabled, 2 templates:
```
1. {"courier": { "service_id": "EP-CS0XXXXXX", "service_name": "..." },"pricing": {"currency": "MYR","total_amount": 6.59,"total_features_price": 1.5,"total_features_tax": 0.09},"features": [{"easytrack_branding": {"enabled": true,"applied_template_id": "EP-ETBTA5","applied_price": 1.5,"applied_tax": 0.09,"available_template": [{ "easytrack_branding_template_id": "EP-ETBTA5", "template_name": "Default", "is_default": true,  "remove_ep_branding": false, "price": 1.5, "discounted_amount": 0, "tax": 0.09 },{ "easytrack_branding_template_id": "EP-ETBTG",  "template_name": "Promo",   "is_default": false, "remove_ep_branding": true,  "price": 2.5, "discounted_amount": 0, "tax": 0.15 }]}}]}
```
### Response Example — account disabled (or per-request ``` enable: false```):
```
1. {"easytrack_branding": {"enabled": false,"applied_template_id": "","applied_price": 0,"applied_tax": 0,"available_template": [{ "easytrack_branding_template_id": "EP-ETBTA5", "template_name": "Default", "is_default": true, "remove_ep_branding": false, "price": 1.5, "discounted_amount": 0, "tax": 0.09 }]}}
```

#### Response Fields - ``` features [].easytrack_branding ```
Field | Type | Description |
----- | ---- | ----------- |
enabled | boolean | Whether EasyTrack Branding will be applied to this shipment if submitted as-is.|
applied_template_id | string | Encoded id **(EP-ETBT...)** of the template that will be auto-applied. Empty string **""** when **enabled = false**.|
applied_price | number | Price of the applied template, after discount. 0 when enabled = false.|
applied_tax | number | Tax on the applied template's price. **0** when **enabled = false**.|
available_template | array | Every template on the account, priced individually (see below). Always populated when the account has at least one template, independent of **enabled**.|

#### ``` available_template [] ``` item
Field | Type | Description |
----- | ---- | ----------- |
easytrack_branding_template_id | string | Encoded id (**EP-ETBT...**). Pass this back in **feature.easytrack_branding.template_id** at submit to choose this template.|
template_name | string | Template name as configured on the Portal.|
is_default | boolean | Whether this is the account's default template (auto-applied when no **template_id** override is given).|
remove_ep_branding | boolean | Whether this template removes the "Powered by EasyParcel" branding (adds **remove_ep_branding_price** to the base price).|
price | number | This template's price after discount.|
discounted_amount | number | Discount amount applied.|
tax | number | Tax on this template's price|

### Important Notes
- If the account has **no** EasyTrack Branding template, this whole feature block is **omitted** from ``` features ``` entirely (not returned as an empty/disabled object).
- ```applied_price``` / ```applied_tax``` / ```applied_template_id``` always describe the **default** (or explicitly-requested) template — not a sum across all templates.
- Prices are returned as JSON **numbers**, rounded to at most 2 decimal places (consistent with ```awb_branding```, ```sms_tracking```, etc. in the same response — no type inconsistency within a quotation).

<h2 id="submit-orders-EasyTrackBranding-2026-06">Submit Orders - EasyTrackBranding </h2>

### Endpoint
```
1.  POST /trunk/shipment/submit_orders
```

### Authentication
OAuth 2.0 with scopes: ``` account:read ```, ``` wallet:read ```, ```wallet:write```,```order:write```


### Request Example - explicit template:
```
1. {"shipment": [{"service_id": "EP-CS0XXXXXX","sender":   { "name": "Sender",   "phone_number_country_code": "60", "phone_number": "123456789", "email": "s@x.com", "address_1": "Jln A", "city": "KL", "postcode": "50000", "country_code": "MY", "subdivision_code": "MY-14" },"receiver": { "name": "Receiver", "phone_number_country_code": "60", "phone_number": "198765432", "email": "r@x.com", "address_1": "Jln B", "city": "George Town", "postcode": "10000", "country_code": "MY", "subdivision_code": "MY-07" },"item": [ { "content": "Books", "value": 100, "weight": 1, "height": 10, "length": 10, "width": 10, "currency_code": "MYR", "quantity": 1 } ],"feature": {"easytrack_branding": { "enable": true, "template_id": "EP-ETBTG" }}}]}
```

#### Request Fields
EasyTrack Branding configuration is specified within the ```feature.easytrack_branding``` object of each shipment item.
Field | Type | Required | Description | Example
--------- | ---- | -------- | ------------|---------
feature.easytrack_branding.enable |boolean| No |  Per-shipment override. Omit to use **account.is_easytrack_branding_enabled**. | TRUE
feature.easytrack_branding.template_id | string | No | The encoded template id (**EP-ETBT...**) from the quotation's **available_template[]**. A **raw numeric** id is also accepted. Omit to use the account's default template. | **"EP-ETBTG"**

#### How It Works
1. The account's default template (```is_default DESC, id ASC```) is resolved once per request.
2. For each shipment, the effective ```enable``` state is: the per-shipment override if present, else ```account.is_easytrack_branding_enabled```.
3. If enabled and ```feature.easytrack_branding.template_id``` is given, that id is decoded (accepts both the ```EP-ETBT...``` encoded form and a raw numeric id) and the matching template — **must belong to the same account** — is looked up. Otherwise the account's default template is used.
4. If a template is found, a ```shipment_easytrack_branding``` record is built and attached to the shipment; pricing (base + ```remove_ep_branding_price``` + discount) and tax (```EASYTRACK_BRANDING```) are then computed and persisted as part of order processing, and the charge is added to the order total.
5. If enabled but the account has no template at all (or the requested ```template_id``` doesn't resolve), branding is **skipped silently** — the order still submits successfully, with no branding charge.

### Response Example :
```
1. {"shipment_easytrack_branding": {"easytrack_branding_template_id": "EP-ETBTG","total_amount": "2.65","price": "2.50","tax_amount": "0.15"}}
```

#### Response Fields - ```shipment_easytrack_branding ```
Returned per shipment in the order-details response (and echoed at submit):
Field | Type | Description |
----- | ---- | ----------- |
easytrack_branding_template_id | string | Encoded id (EP-ETBT...) of the template that was applied.|
total_amount | string | Credit applied for this charge (2 decimal places).|
price | string | Base price charged (2 decimal places).|
tax_amount | string | Tax charged (2 decimal places).|
``` null ``` when no branding was applied to the shipment

### Important Notes
- Payment for the branding charge follows the normal order payment flow — it is included in the shipment/order total the same way ```awb_branding``` is.
- ```feature.easytrack_branding.template_id``` must reference a template **owned by the authenticated account**; a template belonging to another account will not resolve and branding will be skipped (not an error).

<h2 id="order_details-cancel_refund-2026-06">Order Details / Cancel & Refund</h2>
<ul>
  <li>
    <code>POST /trunk/shipment/details</code> — the pricing object of each shipment includes an 
    <code>easytrack_branding</code> field (string, 2 decimal places, or null if not applied), 
    and the branding amount/tax is folded into the shipment's addon totals.
  </li>
  <li>
    <code>POST /trunk/shipment/cancel</code> — cancelling a shipment that has EasyTrack Branding applied 
    automatically refunds the branding charge (credit + tax) back to the account, following the same 
    refund pattern as every other add-on (AWB Branding, insurance, DDP, etc.).
  </li>
</ul>

<h2 id="testing-scenarios-EasyTrackBranding-2026-06">Testing Scenarios</h2>
| # | Setup | Request | Expected |
| --- | --- | --- | --- |
| 1 | is_easytrack_branding_enabled = 1, 2 templates (1 default) | Quotation, no feature override | enabled: true; available_template lists both with encoded ids + per-template price/tax; applied_* reflects the default |
| 2 | Template has remove_ep_branding = 1 | Quotation | That template's price = base + remove_ep_branding_price |
| 3 | is_easytrack_branding_enabled = 0 | Quotation | available_template still lists templates; enabled: false; applied_template_id: ""; applied_price/applied_tax: 0; not folded into total |
| 4 | is_easytrack_branding_enabled = 1 | Quotation with feature.easytrack_branding.enable: false | enabled: false; excluded from total |
| 5 | is_easytrack_branding_enabled = 0 | Quotation with enable: true | enabled: true; included in total |
| 6 | Flag on, default exists | Submit, no feature.easytrack_branding | shipment_easytrack_branding created for the default template; order total includes the charge |
| 7 | Multiple templates | Submit with template_id: "EP-ETBTG" (non-default) | The chosen template is applied & charged — verify the amount matches that template's quoted price |
| 8 | Flag on, no templates on the account | Submit | Order still succeeds; no branding row created; no charge |
| 9 | — | Submit with a raw numeric template_id (e.g. 7) | Accepted — both encoded and raw forms work |
| 10 | Order placed with branding | POST /trunk/shipment/details then POST /trunk/shipment/cancel | Details shows the branding charge + template id; cancel refunds the branding amount |
**Encoding round-trip sanity check:**  
The `easytrack_branding_template_id` returned by scenario 1's quotation, when passed back as `template_id` in scenario 7's submit, must resolve to the same template.
