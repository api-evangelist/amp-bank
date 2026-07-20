---
name: Look up AMP Bank products (CDR PRD)
description: Retrieve and inspect AMP Bank / AMP Bank GO banking products via the public, unauthenticated Consumer Data Right Product Reference Data API.
api: openapi/amp-bank-cds-banking-products-openapi.yml
operations: [listBankingProducts, getBankingProductDetail]
---

# Look up AMP Bank products

The AMP Bank and AMP Bank GO Product Reference Data (PRD) API is public and
unauthenticated. No API key, OAuth token, or credential is required — but every
request MUST carry the CDS version header.

## Base URLs

- AMP Bank (My AMP, BSB 939-200): `https://api.cdr-api.amp.com.au/cds-au/v1`
- AMP Bank GO (BSB 939-900): `https://pub.cdr-sme.amp.com.au/api/cds-au/v1`

## Rules

- Always send `x-v: 5` on `listBankingProducts` and `x-v: 7` on
  `getBankingProductDetail` (the currently supported endpoint versions). Optionally
  send `x-min-v` to negotiate a floor. A missing/invalid version returns `400`; an
  unsupported version returns `406`.
- No `Authorization` header — this is the public PRD surface.
- Responses use CDR pagination: read `meta.totalRecords` / `meta.totalPages` and
  follow `links.next`; page with `page` and `page-size` (default 25).
- Errors arrive as `ResponseErrorListV2` (`{ errors: [ { code, title, detail } ] }`)
  with `urn:au-cds:...` codes — not RFC 9457. See `errors/amp-bank-problem-types.yml`.

## Steps

1. **List products** — call `listBankingProducts` (`GET /banking/products`) with
   `x-v: 5`. Optionally filter with `effective` (CURRENT/FUTURE/ALL),
   `product-category`, `brand`, or `updated-since` for delta polling. Read the
   `data.products[]` array and page via `links.next` until exhausted.
2. **Get product detail** — for a `productId` from step 1, call
   `getBankingProductDetail` (`GET /banking/products/{productId}`) with `x-v: 7`
   to retrieve `features`, `constraints`, `eligibility`, `fees`, `depositRates`,
   and `lendingRates`.
3. **Handle versioning** — on a `406`, lower `x-v` (or set `x-min-v`) to a
   supported version and retry.
