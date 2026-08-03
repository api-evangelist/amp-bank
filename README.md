# AMP Bank (amp-bank)

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
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

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
