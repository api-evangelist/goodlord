---
name: Collect a guarantor and clear referencing conditions
description: >-
  Attach a guarantor to an existing Goodlord application, chase the referee forms, and record
  that the conditions attached to a Conditional Pass have been met. Covers the guarantor
  affordability ratio, the attachedSubjects model and patchSubjectOutcomeConditions.
api: openapi/goodlord-referencing-api-openapi.json
operations:
  - getAuthToken
  - getApplication
  - createSubject
  - getSubject
  - patchSubject
  - patchSubjectOutcomeConditions
  - getSubjectTouchpoints
  - getSubjectEmails
generated: '2026-07-26'
method: generated
source: openapi/goodlord-referencing-api-openapi.json, https://portal.goodlord.co/portal/catalogue-products/referencing-product-1
---

# Collect a guarantor and clear referencing conditions

An applicant who does not meet the affordability threshold on their own usually comes back as
a **Conditional Pass** with a condition such as "guarantor required". This skill covers
attaching that guarantor and recording that the condition is satisfied.

Goodlord also supports **guarantor-only referencing**, where the tenant product is set to
"None" and only the guarantor is assessed.

## Auth

Same as every Goodlord Referencing call: `getAuthToken` (`POST /auth/token`,
`grant_type: client_credentials`) for a one-hour JWT, then
`Authorization: Bearer <token>` **plus** `Company-ID: <your issued Company ID>` on every
request. See `skills/goodlord-reference-a-tenant.md` and
`authentication/goodlord-authentication.yml`.

## Step 1 — Read the application and the failing subject

`getApplication` (`GET /referencing/application/{applicationId}`) returns the application with
its `subjects`. `getSubject` (`GET /referencing/subject/{subjectId}`) on the applicant returns
`outcome`, `milestones` and `recommendations`.

A **Conditional Pass** is the signal to act: the outcome carries the conditions that must be
met before the tenancy can proceed. `recommendations` is where Goodlord tells you what it
thinks is needed.

## Step 2 — Attach the guarantor (`createSubject`)

`PUT /referencing/subject/application/{applicationId}` with subject `type` set to the
guarantor role. Set `rentalDetails` — Goodlord's documented recommendation is an
**affordability ratio of 3 for guarantors** (versus 2.5 for applicants), because the guarantor
is underwriting the whole rent, not just their share.

Link the guarantor to the applicant they are guaranteeing through `attachedSubjects`. That is
the same mechanism used to hang Employer, Accountant and Landlord referees off a subject.

Carry your own identifier in `externalId` so you can reconcile the callback.

## Step 3 — Add referees if required

Employer, Accountant and Landlord referees are themselves subjects created the same way, with
the appropriate `type`, attached to the guarantor. Goodlord issues the reference forms and
emails the referees; you will see `V2.subject.reference.form.generated` when a form is
produced.

## Step 4 — Chase

- `getSubjectEmails` (`GET /referencing/subject/{subjectId}/emails`) — did the referee actually
  receive the request, and what is the delivery status? This is the first thing to check when a
  reference is stuck in **Awaiting Response**.
- `getSubjectTouchpoints` (`GET /referencing/subject/{subjectId}/touchpoints`) — the full
  audit and communication trail, with author and message.
- `patchSubject` (`PATCH /referencing/subject/{subjectId}`) — correct a wrong email address or
  rental detail rather than deleting and recreating the subject.

## Step 5 — Record that conditions are met (`patchSubjectOutcomeConditions`)

`PATCH /referencing/subject/{subjectId}/outcome/conditions` records that the conditions
attached to the outcome have been satisfied.

**Treat this as a consequential write and put a human in front of it.** It changes a
referencing decision on a named individual, which is what a letting agent and a landlord then
rely on to grant or refuse a tenancy. Do not call it automatically off a heuristic; call it
because a person confirmed the condition is genuinely met. This operation is classified as
`acting` in `agentic-access/goodlord-agentic-access.yml`.

## Errors and retries

`400`, `404` and `500` with a plain JSON `APIErrorResponse` envelope — no error codes, no
RFC 9457 problem details. A `404` on a subject id is very often the wrong `Company-ID` header
rather than a missing subject.

There is **no idempotency key** on this API. If a `createSubject` call times out, read the
application back with `getApplication` and check whether the subject already landed before
retrying — otherwise you will attach the same guarantor twice.
