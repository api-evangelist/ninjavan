# Ninja Van (ninjavan)

Ninja Van is a Southeast Asian last-mile logistics and parcel-delivery company operating across Singapore, Malaysia, Indonesia, Philippines, Vietnam, and Thailand. Its **ninjaAPI** lets merchants and e-commerce platforms integrate shipping programmatically: create and cancel delivery orders, generate waybills (AWB), estimate tariffs, look up Ninja Point (PUDO) drop-off locations, receive parcel status updates via webhooks, and pull tracking events.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/ninjavan/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/ninjavan/refs/heads/main/apis.yml)

## Access model (read this first)

Ninja Van's API is **not a self-serve, metered API product** — it is a shipping-integration channel for merchants with a Ninja Van account, and access is gated:

- **Per-country host.** Every request is country-scoped: the country code is the first path segment. Production base URL is `https://api.ninjavan.co/{countryCode}` (e.g. `/SG/`, `/MY/`, `/ID/`, `/PH/`, `/VN/`, `/TH/`). The sandbox is `https://api-sandbox.ninjavan.co/sg` and **only supports the Singapore `sg` country code**.
- **OAuth2 client credentials.** Exchange your `client_id` and `client_secret` for a short-lived access token via `POST /{countryCode}/2.0/oauth/access_token` (grant type `client_credentials`), then send it as `Authorization: Bearer ACCESS_TOKEN` on every request. Cache the token with its expiry and only regenerate within ~5 minutes of expiry or on an HTTP 401.
- **Merchant onboarding + audit.** Sandbox access is requested by email to Ninja Van sales enablement. Production credentials are granted only after passing an **integration audit** (which requires generating sample orders). **Waybill generation requires separate prior access approval.**

Because pricing is per-parcel and country-specific (set in a merchant rate card), there is no public per-call API price; see `plans/` and `finops/`.

## Tags

- Logistics
- Last-Mile Delivery
- Shipping
- Southeast Asia
- Parcels
- Tracking
- Fulfillment
- E-commerce Logistics
- Waybill
- SaaS

## Timestamps

- **Created:** 2026-07-12
- **Modified:** 2026-07-12

## APIs

### Ninja Van OAuth API

Exchange a client ID and client secret for a short-lived OAuth2 access token using the client-credentials grant (`POST /{countryCode}/2.0/oauth/access_token`). The bearer token is attached to every subsequent ninjaAPI request.

- **Human URL:** [https://api-docs.ninjavan.co/](https://api-docs.ninjavan.co/)
- **Base URL:** `https://api.ninjavan.co/{countryCode}`

#### Tags

- OAuth2
- Authentication
- Client Credentials

#### Properties

- [Documentation](https://api-docs.ninjavan.co/)
- [API Reference](https://api-docs.ninjavan.co/)
- [OpenAPI](openapi/ninjavan-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/ninjavan.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/ninjavan.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Ninja Van Order API

Create delivery orders (`POST /{countryCode}/4.2/orders` and the earlier `/4.1/orders`), cancel an order by tracking number (`DELETE /{countryCode}/2.2/orders/{trackingNo}`), and generate domestic or international waybills (`GET /{countryCode}/2.0/reports/waybill` and `/2.0/reports/international-waybills`). Waybill generation requires prior access approval from Ninja Van.

- **Human URL:** [https://api-docs.ninjavan.co/](https://api-docs.ninjavan.co/)
- **Base URL:** `https://api.ninjavan.co/{countryCode}`

#### Tags

- Orders
- Waybill
- AWB
- Shipping

#### Properties

- [Documentation](https://api-docs.ninjavan.co/)
- [API Reference](https://api-docs.ninjavan.co/)
- [OpenAPI](openapi/ninjavan-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/ninjavan.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/ninjavan.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Ninja Van Tracking API

Retrieve tracking events for a single parcel (`GET /{countryCode}/1.0/orders/tracking-events/{trackingNumber}`) or for a list of parcels (`GET /{countryCode}/1.0/orders/tracking-events`). Ninja Van positions webhooks as the primary push mechanism for status changes.

- **Human URL:** [https://api-docs.ninjavan.co/](https://api-docs.ninjavan.co/)
- **Base URL:** `https://api.ninjavan.co/{countryCode}`

#### Tags

- Tracking
- Parcels
- Events

#### Properties

- [Documentation](https://api-docs.ninjavan.co/)
- [API Reference](https://api-docs.ninjavan.co/)
- [OpenAPI](openapi/ninjavan-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/ninjavan.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/ninjavan.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Ninja Van Webhooks API

Ninja Van issues HTTP POST callbacks to a merchant-registered URL on every order status change — Pending Pickup, In Transit, On Vehicle for Delivery, Delivered, Delivery Exception, Returned to Sender, Cancelled, and more. The request body carries JSON describing the event. This is server-to-endpoint HTTP, **not a WebSocket**. Webhook URLs are registered through Ninja Van onboarding.

- **Human URL:** [https://api-docs.ninjavan.co/](https://api-docs.ninjavan.co/)
- **Base URL:** `https://api.ninjavan.co/{countryCode}`

#### Tags

- Webhooks
- Events
- Status Updates

#### Properties

- [Documentation](https://api-docs.ninjavan.co/)
- [OpenAPI](openapi/ninjavan-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)

### Ninja Van Tariff API

Estimate the shipping price for a parcel between an origin and destination (`POST /{countryCode}/1.0/public/price`), given weight and dimensions.

- **Human URL:** [https://api-docs.ninjavan.co/](https://api-docs.ninjavan.co/)
- **Base URL:** `https://api.ninjavan.co/{countryCode}`

#### Tags

- Pricing
- Tariff
- Rate Estimate

#### Properties

- [Documentation](https://api-docs.ninjavan.co/)
- [API Reference](https://api-docs.ninjavan.co/)
- [OpenAPI](openapi/ninjavan-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/ninjavan.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/ninjavan.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Ninja Van PUDO API

List Ninja Point pick-up/drop-off (PUDO) locations (`GET /{countryCode}/2.0/pudos`) and drive shipper drop-off flows for parcels (`/{countryCode}/1.0/send-orders/drop-off` and related send-order endpoints).

- **Human URL:** [https://api-docs.ninjavan.co/](https://api-docs.ninjavan.co/)
- **Base URL:** `https://api.ninjavan.co/{countryCode}`

#### Tags

- PUDO
- Ninja Points
- Drop-off

#### Properties

- [Documentation](https://api-docs.ninjavan.co/)
- [API Reference](https://api-docs.ninjavan.co/)
- [OpenAPI](openapi/ninjavan-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/ninjavan.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/ninjavan.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

## Common Properties

- [Domain Security](security/ninjavan-domain-security.yml)
- [Authentication](authentication/ninjavan-authentication.yml)
- [LinkedIn](https://www.linkedin.com/company/ninja-van)
- [Website](https://www.ninjavan.co/en-sg)
- [Documentation](https://api-docs.ninjavan.co/)
- [Plans](plans/ninjavan-plans-pricing.yml)
- [Rate Limits](rate-limits/ninjavan-rate-limits.yml)
- [Fin Ops](finops/ninjavan-finops.yml)
- [Blog](https://blog.ninjavan.co/en-sg/)

## WebSocket Review

**Does Ninja Van expose a documented public WebSocket API?** No. The ninjaAPI is HTTPS REST plus outbound webhooks (HTTP POST callbacks); no `ws://` or `wss://` endpoint is documented. See [review.yml](review.yml).

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
