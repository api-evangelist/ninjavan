# Ninja Van (ninjavan)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

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
