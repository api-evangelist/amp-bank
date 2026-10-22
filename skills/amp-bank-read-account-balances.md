---
name: amp-bank-read-account-balances
description: Discover a consenting customer's AMP Bank accounts and read their balances via the CDR Banking Accounts and Balances APIs.
api: openapi/amp-bank-banking-accounts-api-openapi.yml
operations: [listBankingAccounts, getBankingAccountDetail, listBankingBalancesBulk, listBankingBalancesSpecificAccounts, getBankingBalance]
---

# Discover a consenting customer's AMP Bank accounts and read their balances

Required CDR scope(s): `bank:accounts.basic:read, bank:accounts.detail:read` (see `scopes/amp-bank-scopes.yml`).

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

1. **List accounts** — `listBankingAccounts` (`GET /banking/accounts`); collect each `accountId`.
2. **Account detail** (optional) — `getBankingAccountDetail` (`GET /banking/accounts/{accountId}`) for BSB/account number, features and rates (needs `bank:accounts.detail:read`).
3. **Balances** — `listBankingBalancesBulk` (`GET /banking/accounts/balances`) for all accounts, `listBankingBalancesSpecificAccounts` (`POST /banking/accounts/balances`) for a chosen set of `accountIds`, or `getBankingBalance` (`GET /banking/accounts/{accountId}/balance`) for one.
