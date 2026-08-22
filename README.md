# Goodlord (goodlord)

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

Goodlord (Oh Goodlord Limited, London) is a United Kingdom PropTech platform that digitises the pre-tenancy and tenancy lifecycle for residential letting agents, landlords and tenants — tenant referencing, e-signed tenancy contracts, rent and deposit payments, rent protection insurance, guarantors, PEPs and sanctions checks, inventories, utility switching and end-of-tenancy. It sits in the middle of the UK rental value chain, between the agency CRM (Reapit, Alto, Street, Qube) and the regulated deposit schemes, insurers and utility suppliers, rather than on the listings side controlled by the Rightmove/Zoopla portal duopoly. Its API posture is unusually open for the UK sector but is honestly split in two — the documentation is genuinely public and the machine-readable contracts are downloadable without a login from a Tyk-powered developer portal at portal.goodlord.co, yet credentials are not self-serve: the portal's own registration page returns "Registration is not allowed" and requires an invite code, and Goodlord's own getting-started guide instructs developers to obtain sandbox and production access through a Goodlord sales manager or account manager. Public contract, partner-gated keys. There is no RESO reference of any kind — RESO is a US NAR/MLS construct with no United Kingdom counterpart — and Goodlord publishes no open data.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/goodlord/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/goodlord/refs/heads/main/apis.yml)

## Tags

- Real Estate
- United Kingdom
- PropTech
- Property Management
- Rentals
- Lettings
- Tenant Referencing
- Tenancy Management
- Insurance
- Payments

## Timestamps

- **Created:** 2026-07-26
- **Modified:** 2026-07-26

## APIs

### Goodlord Referencing API

Goodlord's public Referencing API — the production surface of the Referencing Product listed in the public catalogue of the Goodlord Developer Portal. It lets a lettings agency's own system create rental applications, add and assess Applicants and Guarantors (plus Employer, Accountant and Landlord referees) through the referencing process, patch outcome conditions, read touchpoints and emails, and retrieve generated documents. Authentication is OAuth 2.0 machine-to-machine client_credentials against /auth/token, returning a one-hour JWT bearer token; every call additionally carries an issued Company-ID header. Three webhook events are documented (V2.subject.report.generated, V2.subject.reference.form.generated, V2.subject.outcome.updated) but subscriptions are configured by Goodlord on request, not self-serve. The OpenAPI 3.1.0 document was fetched anonymously; credentials are issued only through a Goodlord account manager.

- **Human URL:** [https://portal.goodlord.co/portal/catalogue-products/referencing-product-1](https://portal.goodlord.co/portal/catalogue-products/referencing-product-1)
- **Base URL:** `https://api.goodoverlord.com`

#### Tags

- Referencing
- Tenant Screening
- Applications
- Lettings
- Rentals

#### Properties

- [OpenAPI](openapi/goodlord-referencing-api-openapi.json) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Documentation](https://portal.goodlord.co/portal/catalogue-products/referencing-product-1)
- [API Reference](https://portal.goodlord.co/portal/catalogue-products/referencing-product-1/dHlrL3Byb2QtcmVmZXJlbmNpbmctYXBp/docs)
- [Getting Started](https://portal.goodlord.co/blog/2024/8/22/getting-started-with-goodlords-referencing-api)
- [Documentation](https://portal.goodlord.co/blog/2024/8/20/getting-started-with-goodlord-referencing-api)

### Goodlord Referencing API (Sandbox)

The sandbox environment of the Goodlord Referencing Product, published as a separate entry in the developer portal's public catalogue and carrying its own OpenAPI 3.1.0 document with the sandbox server and sandbox token endpoint. Operation surface is identical to the live API. Goodlord's getting-started guide states that a sandbox account is arranged by Goodlord's team during a commercial engagement and that production is enabled afterwards by an account manager, so this is a partner sandbox rather than an open trial — no self-serve key issuance exists.

- **Human URL:** [https://portal.goodlord.co/portal/catalogue-products/referencing-product-1](https://portal.goodlord.co/portal/catalogue-products/referencing-product-1)
- **Base URL:** `https://api-sandbox.goodlord.co`

#### Tags

- Referencing
- Sandbox
- Tenant Screening
- Lettings

#### Properties

- [OpenAPI](openapi/goodlord-referencing-api-sandbox-openapi.json) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Documentation](https://portal.goodlord.co/portal/catalogue-products/referencing-product-1)
- [API Reference](https://portal.goodlord.co/portal/catalogue-products/referencing-product-1/dHlrL3Byb2Qtc2FuZGJveC1yZWZlcmVuY2luZy1hcGk/docs)

### Goodlord Insurance App API

A second real Goodlord API surface, discovered outside the developer portal. The Goodlord Insurance App is an API Platform (Symfony) service whose OpenAPI 3.1.0 document is served publicly and unauthenticated at /api/v1/docs with the application/vnd.openapi+json media type. It covers rent protection insurance claims handling — insurance claims and claim submission, claim file upload and deletion, claim payments, rent schedules and rent schedule rows, plus agents, companies, roles and role groups. All 21 operations are gated by a JWT in the Authorization header and every collection probe returned HTTP 401. Goodlord does not list this API in its developer portal catalogue and publishes no onboarding path for it, so the contract is public but the API itself is an internal application surface, not an offered developer product.

- **Human URL:** [https://insurance-app.goodlord.co/api/v1/docs](https://insurance-app.goodlord.co/api/v1/docs)
- **Base URL:** `https://insurance-app.goodlord.co`

#### Tags

- Insurance
- Rent Protection
- Claims
- Payments
- Rent Schedule

#### Properties

- [OpenAPI](openapi/goodlord-insurance-app-api-openapi.json) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [API Reference](https://insurance-app.goodlord.co/api/v1/docs)

## Common Properties

- [Website](https://www.goodlord.com/)
- [Developer Portal](https://portal.goodlord.co/)
- [Documentation](https://portal.goodlord.co/portal/catalogue-products)
- [Blog](https://www.goodlord.com/newsagent)
- [Blog](https://portal.goodlord.co/blog)
- [Authentication](https://portal.goodlord.co/portal/catalogue-products/referencing-product-1)
- [OpenID Connect Discovery](https://login.goodlord.co/7ddbafdc-ee33-46fb-968a-3011e2a0a825/B2C_1A_2_SIGNUPORSIGNIN/v2.0/.well-known/openid-configuration)
- [Login](https://app.goodlord.co/)
- [Partners](https://www.goodlord.com/about/our-partners)
- [Integrations](https://www.goodlord.com/platform/integrations)
- [Pricing](https://www.goodlord.com/platform)
- [LinkedIn](https://www.linkedin.com/company/goodlord)
- [Contact](https://www.goodlord.com/contact-us)

## Maintainers

- **Kin Lane** — kin@apievangelist.com
