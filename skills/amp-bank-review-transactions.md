---
name: amp-bank-review-transactions
description: Pull and inspect transaction history for a consenting customer's AMP Bank account via the CDR Banking Transactions API.
api: openapi/amp-bank-banking-account-transactions-api-openapi.yml
operations: [listBankingTransactions, getBankingTransactionDetail]
---

# Pull and inspect transaction history for a consenting customer's AMP Bank account

Required CDR scope(s): `bank:transactions:read` (see `scopes/amp-bank-scopes.yml`).

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

1. Obtain an `accountId` (see `amp-bank-read-account-balances`).
2. **List transactions** — `listBankingTransactions` (`GET /banking/accounts/{accountId}/transactions`), filtering with `oldest-time` / `newest-time`, `min-amount` / `max-amount` or `text`; page through `links.next`.
3. **Transaction detail** — for entries with `isDetailAvailable: true`, call `getBankingTransactionDetail` (`GET /banking/accounts/{accountId}/transactions/{transactionId}`) for extended payment data.
