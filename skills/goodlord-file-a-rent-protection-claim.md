---
name: File a rent protection insurance claim with Goodlord
description: >-
  Create a rent protection insurance claim, build the arrears rent schedule, attach evidence
  files and submit the claim using the Goodlord Insurance App API. Covers the API Platform
  pagination and filtering conventions, JSON:API/problem+json error handling and the two
  irreversible submit operations.
api: openapi/goodlord-insurance-app-api-openapi.json
operations:
  - get_me
  - api_insurance_claims_get_collection
  - api_insurance_claims_post
  - api_insurance_claims_id_get
  - api_insurance_claims_id_patch
  - api_insurance_claims_insuranceClaimIdrent_schedule_get
  - api_insurance_claims_insuranceClaimIdrent_schedule_rentScheduleIdrent_schedule_rows_post
  - api_insurance_claims_insuranceClaimIdrent_schedule_rentScheduleIdrent_schedule_row_id_patch
  - api_insurance_claims_insuranceClaimIdrent_schedule_rentScheduleIdsubmit_post
  - api_insurance_claims_insuranceClaimIdfiles_post
  - api_insurance_claims_idsubmit_post
  - api_insurance_claims_insuranceClaimIdpayments_get_collection
generated: '2026-07-26'
method: generated
source: openapi/goodlord-insurance-app-api-openapi.json
---

# File a rent protection insurance claim with Goodlord

The Goodlord Insurance App handles rent protection insurance claims: a letting agent records
the arrears, attaches evidence, submits to the insurer and tracks the payments that come back.

## Before you start

**This API is not an offered developer product.** Its OpenAPI 3.1.0 document is served
publicly and unauthenticated at `https://insurance-app.goodlord.co/api/v1/docs`, but it is not
listed in Goodlord's developer portal catalogue and Goodlord publishes no onboarding path for
it. Every data operation returns `401` without a token. Do not attempt to obtain access
outside a commercial relationship with Goodlord.

Authentication is a **JWT bearer in the `Authorization` header**. The spec declares it as
`type: apiKey` in the header rather than `type: http, scheme: bearer` — a modelling quirk, not
a different runtime behaviour. No token endpoint, authorization server or scope surface is
published for this API.

Confirm who you are with `get_me` (`GET /api/v1/me`) — it returns the calling agent's
`companies`, `roles` and `roleGroups`. Everything you can see is scoped by those companies.

## Conventions on this surface

Unlike the Referencing API, this is a generated **API Platform (Symfony)** service:

- **Pagination**: `page` and `itemsPerPage` query parameters.
- **Filtering**: `claimStatus`, `claimStatus[]`, `company.externalId`,
  `policyUniqueReferenceNumber`, `propertyAddress`.
- **Sorting**: `order[claimDate]`, `order[latestPaymentDate]`, `order[totalPaymentAmount]`.
- **Expansion**: `include` for JSON:API compound documents.
- **Representations**: `application/ld+json` (Hydra), `application/vnd.api+json` (JSON:API),
  `application/json` and `text/csv`. Content negotiation is strict — the wrong `Accept` gets a
  `406`.
- **No idempotency key** on any of the 35 operations.

Full detail in `conventions/goodlord-conventions.yml`.

## Step 1 — Find or create the claim

`api_insurance_claims_get_collection` (`GET /api/v1/insurance_claims`) with
`claimStatus` and `company.externalId` filters to check whether a claim already exists for the
tenancy before you create a duplicate — there is no idempotency key to protect you.

`api_insurance_claims_post` (`POST /api/v1/insurance_claims`) creates the claim. The
`InsuranceClaim` entity is very wide (130+ fields) and spans the whole UK possession-proceedings
timeline — Section 8 and Section 21 notice served and expired dates, proceedings issued,
hearing date, possession date, warrants, eviction date — plus deposit handling and the
compliance evidence trail (gas safety certificates, EPC, EICR, How to Rent guides) and the
Renters' Rights Act fields (`rraInfoSheetIssueDate`, `statementOfTermsIssuedDate`). Set your
own reference in `externalId`. See `data-model/goodlord-data-model.yml`.

`api_insurance_claims_id_patch` (`PATCH /api/v1/insurance_claims/{id}`) updates it. PATCH uses
JSON merge patch representations on this service.

## Step 2 — Build the rent schedule

`api_insurance_claims_insuranceClaimIdrent_schedule_get`
(`GET /api/v1/insurance_claims/{insuranceClaimId}/rent_schedule`) returns the single schedule
attached to the claim — one claim has exactly one schedule.

Add the arrears lines with
`api_insurance_claims_insuranceClaimIdrent_schedule_rentScheduleIdrent_schedule_rows_post`
(the bulk `rent_schedule_rows` endpoint) rather than one call per row. Each row carries
`rowType`, `date`, `amount` and a running `balance`, and keeps its own `audits` trail.

Correct a row with the `..._rent_schedule_row_id_patch` operation and remove one with
`..._rent_schedule_row_id_delete` — rows are soft-deleted (`deletedAt`), so the audit trail
survives.

**Reconcile the schedule against the claim's arrears fields** (`dateOfRentArrears`,
`rentOutstanding`, `firstArrearsDate`) before submitting. The insurer pays against the
schedule.

## Step 3 — Attach evidence

`api_insurance_claims_insuranceClaimIdfiles_post`
(`POST /api/v1/insurance_claims/{insuranceClaimId}/files`) uploads a file. List with the
matching `..._files_get_collection`, remove with `..._files_id_delete`.

Evidence is the claim: tenancy agreement, notices served, correspondence, compliance
certificates. Check the claim's document fields (`gasSafetyCertificates`, `howToRentGuides`,
`didUploadEpcToGoodlord`) against what you have actually attached.

## Step 4 — Submit (irreversible, human-in-the-loop)

Two submit operations, in order:

1. `api_insurance_claims_insuranceClaimIdrent_schedule_rentScheduleIdsubmit_post` — submits the
   rent schedule (sets `submittedAt`).
2. `api_insurance_claims_idsubmit_post` (`POST /api/v1/insurance_claims/{id}/submit`) — submits
   the claim to the insurer.

**Both are consequential and neither should be called by an agent unattended.** A submitted
claim is a financial and legal assertion about a named tenant in an active possession process.
Get an explicit human confirmation, and confirm the schedule totals and the evidence list back
to that human before you call either. See `agentic-access/goodlord-agentic-access.yml`.

## Step 5 — Track payments

`api_insurance_claims_insuranceClaimIdpayments_get_collection`
(`GET /api/v1/insurance_claims/{insuranceClaimId}/payments`) lists insurer payments with
`paymentStatusIdentifier`, `paymentStatusDescription`, `paymentAmount` and the
`paymentSubmittedAt` / `paymentPaidAt` timeline. Payments are **read-only** over the API — you
cannot create or amend one.

There is **no webhook or event surface on this API at all**. Claim status, rent schedule status
and payment status are poll-only. Sort with `order[latestPaymentDate]` and filter by
`claimStatus` rather than walking every claim.

## Errors

RFC 9457 `application/problem+json` (and JSON:API `Error.jsonapi`) on **400**, **403**, **404**
and **422**. A `422` carries `ConstraintViolation` — per-field validation failures; read the
violations and fix the specific fields rather than resubmitting the whole payload unchanged. A
`403` on a collection usually means the resource belongs to a company outside your agent's
`companies`. Catalogue: `errors/goodlord-problem-types.yml`.
