---
name: amp-bank-review-regular-payments
description: Review a consenting customer's direct debits, scheduled payments and instalment plans at AMP Bank via the CDR Banking APIs.
api: openapi/amp-bank-banking-account-scheduled-payments-api-openapi.yml
operations: [listDirectDebits, listDirectDebitsBulk, listDirectDebitsSpecificAccounts, listScheduledPayments, listScheduledPaymentsBulk, listScheduledPaymentsSpecificAccounts, listInstalmentPlans, listInstalmentPlansBulk]
---

# Review a consenting customer's direct debits, scheduled payments and instalment plans at AMP Bank

Required CDR scope(s): `bank:regular_payments:read` (see `scopes/amp-bank-scopes.yml`).

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

Direct-debit operations live in `openapi/amp-bank-banking-account-direct-debits-api-openapi.yml`; scheduled payments and instalment plans in `openapi/amp-bank-banking-account-scheduled-payments-api-openapi.yml`.

1. **Direct debits** — `listDirectDebits` (one account), `listDirectDebitsBulk` (all), or `listDirectDebitsSpecificAccounts` (`POST /banking/accounts/direct-debits` with `accountIds`).
2. **Scheduled payments** — `listScheduledPayments`, `listScheduledPaymentsBulk` or `listScheduledPaymentsSpecificAccounts`.
3. **Instalment plans** — `listInstalmentPlans` (`GET /banking/accounts/{accountId}/payments/plans`) or `listInstalmentPlansBulk`.
