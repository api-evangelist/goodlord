---
name: Reference a tenant with Goodlord
description: >-
  Create a rental application, add an applicant, track the referencing outcome and retrieve the
  final report using the Goodlord Referencing API. Covers OAuth client_credentials auth, the
  mandatory Company-ID tenant header, the outcome state machine and the webhook-then-read
  pattern.
api: openapi/goodlord-referencing-api-openapi.json
operations:
  - getAuthToken
  - createApplication
  - createSubject
  - getSubject
  - getSubjectTouchpoints
  - getSubjectEmails
  - getAuthenticatedFile
generated: '2026-07-26'
method: generated
source: openapi/goodlord-referencing-api-openapi.json, https://portal.goodlord.co/portal/catalogue-products/referencing-product-1
---

# Reference a tenant with Goodlord

Goodlord's Referencing API assesses applicants and guarantors for a UK residential tenancy.
You create an **Application** (the tenancy), attach **Subjects** (the people), and Goodlord
runs identity, income, affordability, residential and credit checks and produces an
**outcome** and a **report**.

## Before you start

- **Credentials are not self-serve.** `client_id`, `client_secret` and your `Company-ID` are
  issued by a Goodlord account manager. The developer portal's registration page returns
  "Registration is not allowed". Do not attempt to sign up programmatically.
- Work in **sandbox** first: `https://api-sandbox.goodlord.co`. Live is
  `https://api.goodoverlord.com`. The operation surface is identical; only the host and token
  URL differ. See `sandbox/goodlord-sandbox.yml`.
- **This is high-sensitivity personal data** — identity documents, income, affordability and
  credit outcomes on named individuals. Never echo subject documents or report contents into a
  transcript, log or third-party tool. Retrieve a document only when a human has asked for it.

## Step 1 — Get a token (`getAuthToken`)

`POST /auth/token` with a JSON body carrying `client_id`, `client_secret` and
`grant_type: "client_credentials"`.

The response is `{ "token_type": "Bearer", "expires_in": 3600, "access_token": "...",
"scope": "free_plan referencing_product" }`. The token is a JWT valid for **one hour** —
cache it and refresh on expiry rather than minting one per call.

**Every subsequent request carries three headers:**

```
Authorization: Bearer <access_token>
Company-ID: <your issued Company ID>
Content-Type: application/json
```

`Company-ID` is mandatory and is **not declared in the OpenAPI** — it only appears in the
portal's Authentication walkthrough. Omitting it is the most common cause of a 403.

## Step 2 — Create the application (`createApplication`)

`POST /referencing/application` with the tenancy and rental information. The response carries
the `id` you use as `applicationId` everywhere below.

**There is no idempotency key** on this API (`conventions/goodlord-conventions.yml`). A
retried `POST` creates a second application. If a create times out, call `getApplication`
against any id you were returned before retrying — never retry blind.

## Step 3 — Add the applicant (`createSubject`)

`PUT /referencing/subject/application/{applicationId}`. Note it is a **PUT against the parent
application**, not a POST to a subject collection. Set the subject `type` to the role being
assessed — the published set is Applicant, Guarantor, Employer referee, Accountant referee and
Landlord referee. Referees hang off an applicant or guarantor via `attachedSubjects`.

`rentalDetails` carries the price share and affordability ratio. Goodlord's documented
recommendation is an affordability ratio of **2.5 for applicants** and **3 for guarantors**.

Use `externalId` to carry your own system's identifier — it is the only caller-supplied
correlation field in the contract.

## Step 4 — Track progress

Two ways, and you should use both:

- **Webhooks (preferred).** Goodlord publishes three events:
  `V2.subject.reference.form.generated`, `V2.subject.outcome.updated` and
  `V2.subject.report.generated`. The payload carries identifiers only
  (`data.customerId`, `data.applicationId`, `data.subjectId`, `data.type`) — you always read
  state back over REST. Subscriptions are configured by Goodlord on request; there is no
  subscription API. **No signature scheme is published**, so treat a delivery as an untrusted
  hint to go and read, never as authoritative state. See
  `asyncapi/goodlord-referencing-webhooks.yml`.
- **Polling `getSubject`.** `GET /referencing/subject/{subjectId}` returns the current
  `outcome`, `milestones` and `recommendations`. Published outcome states are **Pending
  Submission, In Review, Awaiting Response, Accepted, Rejected, Cancelled**; outcome kinds are
  **Pass, Conditional Pass, Fail**. No rate limits are published — poll conservatively.

`getSubjectTouchpoints` (`GET /referencing/subject/{subjectId}/touchpoints`) gives the audit
and communication trail; `getSubjectEmails` (`GET /referencing/subject/{subjectId}/emails`)
shows what Goodlord emailed the subject and whether it was delivered — that is where you look
when a subject "hasn't heard anything".

## Step 5 — Retrieve the report (`getAuthenticatedFile`)

On `V2.subject.report.generated`, call
`GET /referencing/media/document/{documentId}` to obtain an authenticated file URL. Document
types published are identity, income, residential, credit and output report. The URL is
short-lived — fetch it and hand it to the human immediately; do not store it.

## Errors

The Referencing API returns a plain JSON `APIErrorResponse` envelope (not RFC 9457) on
**400**, **404** and **500**. There are no error codes — only a message. Full catalogue:
`errors/goodlord-problem-types.yml`.

- **400** — malformed body or missing required field. Do not retry unchanged.
- **404** — wrong id, or the resource belongs to a different `Company-ID`. Check the tenant header.
- **500** — retry with backoff, but see the idempotency warning above before retrying a write.

There is no `429` declared and no rate-limit headers, so back off on any repeated failure
rather than assuming capacity.
