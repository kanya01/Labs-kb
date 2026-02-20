---
title: API Overview — live.o REST API
type: doc
status: current
linked-repo: https://github.com/kanya01/COLABS
linked-pr: ""
linked-issue: ""
tags: [api, rest, backend, rails]
updated: 2026-02-20
---

# API Overview — live.o REST API

> Source: [docs/api/API_OVERVIEW.md](https://github.com/kanya01/COLABS/blob/main/docs/api/API_OVERVIEW.md)

REST API reference for the Rails 8 backend. All endpoints require a `Bearer <JWT>` header except public discovery and auth routes.

---

## Base URL

- **Dev**: `http://localhost:4000`
- **Prod**: `https://liveo.space` (API routes under `/api/v1/`)

---

## Key Resource Groups

| Resource | Description |
|---|---|
| `/auth` | JWT issuance, Auth0 callback, logout |
| `/users` | User profiles, avatar upload |
| `/services` | Service CRUD with nested tier attributes |
| `/orders` | Order lifecycle — create, state transitions, deliverables |
| `/conversations` | Conversation list and creation |
| `/messages` | Messages within a conversation |
| `/notifications` | Notification list, mark-read |
| `/stripe` | PaymentIntent creation, Connect onboarding, payout requests |
| `/webhooks/stripe` | Stripe webhook receiver |
| `/subscribers` | Newsletter sign-up and confirmation |

---

## Authentication

- JWT tokens issued on login, 24-hour expiry
- All protected routes require: `Authorization: Bearer <token>`
- Auth0 handles OAuth social flows (Google, GitHub)

See [[Docs/api/AUTH0_SETUP]] for Auth0 configuration.

---

## Related Notes

- [[Docs/design/SYSTEM_ONTOLOGY]] — Full entity and field reference
- [[Docs/services/STRIPE_INTEGRATION]] — Stripe-specific endpoint details
- [[_System Map/Architecture]] — System overview
