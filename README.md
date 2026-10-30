# Goodlord

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

**Areas:** Real Estate · United Kingdom · PropTech · Property Management · Rentals · Lettings · Tenant Referencing · Tenancy Management · Insurance · Payments

## Goodlord on APIs.io

Everything profiled for Goodlord is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/goodlord/](https://apis.io/providers/goodlord/)** — or go straight to one of the APIs or properties below.

### APIs (15)

- [Goodlord Agent API](https://apis.io/apis/goodlord/goodlord-agent-api/) — Resource 'Agent' operations.
- [Goodlord Application API](https://apis.io/apis/goodlord/goodlord-application-api/) — An application contains rental information and all of the applicants/guarantors which are applying for a tenancy.
- [Goodlord Authentication API](https://apis.io/apis/goodlord/goodlord-authentication-api/) — Authentication operations
- [Goodlord Company API](https://apis.io/apis/goodlord/goodlord-company-api/) — Resource 'Company' operations.
- [Goodlord File API](https://apis.io/apis/goodlord/goodlord-file-api/) — Resource 'File' operations.
- [Goodlord Insurance Claim API](https://apis.io/apis/goodlord/goodlord-insuranceclaim-api/) — Resource 'InsuranceClaim' operations.
- [Goodlord Media API](https://apis.io/apis/goodlord/goodlord-media-api/) — Operations which are concerned around retrieving files
- [Goodlord Payment API](https://apis.io/apis/goodlord/goodlord-payment-api/) — Resource 'Payment' operations.
- [Goodlord Rent Schedule API](https://apis.io/apis/goodlord/goodlord-rentschedule-api/) — Resource 'RentSchedule' operations.
- [Goodlord Rent Schedule Row API](https://apis.io/apis/goodlord/goodlord-rentschedulerow-api/) — Resource 'RentScheduleRow' operations.
- [Goodlord Rent Schedule Row Post Dto API](https://apis.io/apis/goodlord/goodlord-rentschedulerowpostdto-api/) — Resource 'RentScheduleRowPostDto' operations.
- [Goodlord Rent Schedule Row Update API](https://apis.io/apis/goodlord/goodlord-rentschedulerowupdate-api/) — Resource 'RentScheduleRowUpdate' operations.
- [Goodlord Role API](https://apis.io/apis/goodlord/goodlord-role-api/) — Resource 'Role' operations.
- [Goodlord Role Group API](https://apis.io/apis/goodlord/goodlord-rolegroup-api/) — Resource 'RoleGroup' operations.
- [Goodlord Subject API](https://apis.io/apis/goodlord/goodlord-subject-api/) — A person who exists on an application.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Goodlord Referencing Webhooks](https://apis.io/asyncapis/goodlord/goodlord-referencing-webhooks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [goodlord](https://apis.io/servers/goodlord/goodlord/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Goodlord Agentic Access](https://apis.io/agentic-access/goodlord/goodlord-agentic-access/)

#### Collections (3)

Postman and Open Collection request collections.

- [Insurance App](https://apis.io/collections/goodlord/open-goodlord-insurance-app-api/)
- [Referencing API](https://apis.io/collections/goodlord/open-goodlord-referencing-api/)
- [Referencing API](https://apis.io/collections/goodlord/open-goodlord-referencing-api-sandbox/)

#### Overlays (3)

OpenAPI overlays, including conversational phrasing for each operation.

- [Goodlord Insurance App Api Overlay](https://apis.io/overlays/goodlord/goodlord-insurance-app-api-overlay/)
- [Goodlord Referencing Api Overlay](https://apis.io/overlays/goodlord/goodlord-referencing-api-overlay/)
- [Goodlord Referencing Api Sandbox Overlay](https://apis.io/overlays/goodlord/goodlord-referencing-api-sandbox-overlay/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Goodlord Authentication](https://apis.io/security/goodlord/goodlord-authentication/)
- [Goodlord Domain Security](https://apis.io/security/goodlord/goodlord-domain-security/)
- [Goodlord Trust Center](https://apis.io/security/goodlord/goodlord-trust-center/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Goodlord Scopes](https://apis.io/scopes/goodlord/goodlord-scopes/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Goodlord Plans Pricing](https://apis.io/plans/goodlord/goodlord-plans-pricing/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.goodlord.com/)
- [Documentation](https://portal.goodlord.co/portal/catalogue-products)
- [Getting started](https://portal.goodlord.co/blog/2024/8/22/getting-started-with-goodlords-referencing-api)
- [API reference](https://portal.goodlord.co/portal/catalogue-products/referencing-product-1/dHlrL3Byb2QtcmVmZXJlbmNpbmctYXBp/docs)
- [Pricing](https://www.goodlord.com/platform)
- [Support](https://www.goodlord.com/support)
- [Blog](https://www.goodlord.com/newsagent)
- [Compliance](https://trust.goodlord.com/)
- [Terms of service](https://www.goodlord.com/terms)
- [Privacy policy](https://www.goodlord.com/privacy-policy)
- [Status](https://goodlord.statuspal.io/)

## API Evangelist rating

**Kin Score 56.7** — strong · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 71.4 |
| Contract quality | 61.3 |
| Contract governance | 4.5 |
| Operational transparency | 23.7 |
| Developer ergonomics | 70.4 |
| Access clarity | 53.9 |

**Agent readiness 33.8** — agent-ready

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | — |
| MCP Server | — |
| Auth Clarity | served (partial credit) |
| Idempotency | — |
| Error Semantics | verified |
| OpenAPI Examples | partial |
| Rate Limit Signal | — |
| Event Surface Described | yes |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | — |
| Operation Distinctiveness | mostly |

**Regulatory alignment 41.2** — Insurance

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/goodlord/](https://apis.io/providers/goodlord/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Goodlord: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/goodlord/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
