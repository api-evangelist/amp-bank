# AMP Bank (amp-bank)

AMP Bank Limited is the retail and business banking arm of AMP Limited (ASX:AMP), a diversified Australian financial services group operating since 1849 and headquartered in Sydney. AMP Bank is a publicly listed (shareholder-owned, not a mutual) authorised deposit-taking institution (ADI) regulated by APRA, offering home loans, deposit and savings accounts, and the digital AMP Bank GO small-business and everyday banking brand. As an active ADI, AMP participates in Australia's Consumer Data Right (CDR / Open Banking) regime and exposes public, unauthenticated Product Reference Data (PRD) APIs conforming to the DSB Consumer Data Standards.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/amp-bank/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/amp-bank/refs/heads/main/apis.yml)

## Tags

- Financial
- Banks
- Open Banking
- CDR
- Consumer Banking
- Australia
- Product Reference Data
- ADI

## Timestamps

- **Created:** 2026-07-20
- **Modified:** 2026-07-20

## APIs

### AMP Bank CDR Product Reference Data API

Public, unauthenticated Consumer Data Right Product Reference Data (PRD) API for the My AMP retail banking brand (BSB 939-200). Serves `GET /banking/products` and `/banking/products/{productId}` conforming to the DSB Consumer Data Standards. Confirmed live returning HTTP 200 (x-v 4) with eight AMP Bank products including home loans, savings and term deposits. Requires the CDS `x-v` version header; no authentication.

- **Human URL:** [https://www.amp.com.au/personal-banking/open-banking/open-banking-api](https://www.amp.com.au/personal-banking/open-banking/open-banking-api)
- **Base URL:** `https://api.cdr-api.amp.com.au/cds-au/v1`

#### Tags

- CDR
- Open Banking
- Product Reference Data
- Banking
- Australia

#### Properties

- [Documentation](https://www.amp.com.au/personal-banking/open-banking/open-banking-api)
- [API Reference](https://consumerdatastandardsaustralia.github.io/standards/#get-products)
- [OpenAPI](openapi/amp-bank-cds-banking-products-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)

### AMP Bank GO CDR Product Reference Data API

Public, unauthenticated Consumer Data Right Product Reference Data (PRD) API for the AMP Bank GO digital small-business and everyday banking brand (BSB 939-900). Confirmed live returning HTTP 200 (x-v 4 and 5) with nine AMP Bank GO products including business save, everyday and term deposit accounts, conforming to the DSB Consumer Data Standards. Requires the CDS `x-v` version header; no authentication.

- **Human URL:** [https://www.amp.com.au/personal-banking/open-banking/open-banking-api](https://www.amp.com.au/personal-banking/open-banking/open-banking-api)
- **Base URL:** `https://pub.cdr-sme.amp.com.au/api/cds-au/v1`

#### Tags

- CDR
- Open Banking
- Product Reference Data
- Small Business
- Australia

#### Properties

- [Documentation](https://www.amp.com.au/personal-banking/open-banking/open-banking-api)
- [API Reference](https://consumerdatastandardsaustralia.github.io/standards/#get-products)
- [OpenAPI](openapi/amp-bank-cds-banking-products-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)

## CDR / Open Banking Notes

AMP Bank's public API surface is its Consumer Data Right **Product Reference Data (PRD)** endpoints — one per brand — which return banking product data without authentication (only the CDS `x-v` version header is required). The broader CDR consumer data sharing surface (accounts, balances, transactions) is not public; it is gated behind the CDR Accredited Data Recipient (ADR) model using OAuth2/OIDC with the FAPI 1.0 Advanced profile, MTLS, and PAR.

The harvested OpenAPI in `openapi/` is the **shared DSB Consumer Data Standards "CDR Banking API" (v1.36.0)**, not an AMP-proprietary contract — AMP conforms to this common standard rather than publishing its own spec.

## Common Properties

- [Website](https://www.amp.com.au/)
- [Documentation](https://www.amp.com.au/personal-banking/open-banking/open-banking-api)
- [LinkedIn](https://www.linkedin.com/company/amp)
- [Terms of Service](https://www.amp.com.au/terms-and-conditions)
- [Privacy Policy](https://www.amp.com.au/privacy)
- [Support](https://www.amp.com.au/help-and-support)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
