---
name: amp-bank-list-payees
description: List and inspect the saved payees of a consenting AMP Bank customer via the CDR Banking Payees API.
api: openapi/amp-bank-banking-payees-api-openapi.yml
operations: [listBankingPayees, getBankingPayeeDetail]
---

# List and inspect the saved payees of a consenting AMP Bank customer

Required CDR scope(s): `bank:payees:read` (see `scopes/amp-bank-scopes.yml`).

## Rules

- These are CDR **consumer-data** endpoints. They are callable only by an
  ACCC-accredited data recipient holding an active customer consent: mTLS plus a
  FAPI OAuth 2.0 access token (see `authentication/amp-bank-authentication.yml`).
  There is no sandbox and no public credential.
- The base URI in the contract (`mtls.dh.example.com`) is the CDS placeholder; AMP's
  real data-holder resource URI comes from the CDR Register.
- Send `x-v` (and optionally `x-min-v`) on every call; a missing version returns
  `400`, an unsupported one `406`. Send `x-fapi-interaction-id` (UUID) and, when the
  customer is present, `x-fapi-auth-date` / `x-fapi-customer-ip-address`.
- All operations are read-only (GET, or POST used as a filtered read), so
  idempotency keys do not apply; retries are safe.
- Page with `page` / `page-size` and follow `links.next`.
- Errors arrive as `ResponseErrorListV2` with `urn:au-cds:...` codes — see
  `errors/amp-bank-problem-types.yml`.

## Steps

1. **List payees** — `listBankingPayees` (`GET /banking/payees`), optionally filtering by `type` (DOMESTIC, INTERNATIONAL, BILLER, DIGITAL_WALLET).
2. **Payee detail** — `getBankingPayeeDetail` (`GET /banking/payees/{payeeId}`) for account/BPAY/PayID/international details.
