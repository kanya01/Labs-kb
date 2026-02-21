
---
title: Architecture — live.o Music Collaboration Platform
type: system-map
status: current
linked-repo: https://github.com/kanya01/COLABS
linked-pr: ""
linked-issue: ""
tags: [architecture, system-map, live-o, colabs]
updated: 2026-02-20
---

# Architecture — live.o Music Collaboration Platform

> **Repo**: [kanya01/COLABS](https://github.com/kanya01/COLABS)
> **Live**: `liveo.space` (deployed on Fly.io)
> **Last updated**: 2026-02-20

---

## System Overview

live.o is a **music collaboration marketplace** — connecting musicians, producers, and audio engineers so they can discover each other, offer tiered services, transact securely, and communicate around orders. It is a full-stack monorepo with a **Next.js** frontend and a **Ruby on Rails** API backend, connected by REST and backed by PostgreSQL.

---

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | Next.js 15, React 19, Tailwind CSS, Framer Motion |
| State / Data | Zustand (client state), React Query (server state) |
| Backend | Ruby on Rails 8 (API-only mode) |
| Database | PostgreSQL |
| Auth | Auth0 (JWT, 24-hr expiry; Google + GitHub OAuth) |
| Payments | Stripe (PaymentIntent + Connect for seller payouts) |
| Email | Resend (API-based, branded templates) |
| Job Queue | SolidQueue (async email delivery) |
| File Storage | Active Storage (deliverables, portfolio items) |
| Deployment | Fly.io — Docker containers, CI/CD via GitHub Actions |
| Language | TypeScript (frontend), Ruby (backend) |

---

## Core Components

### 1. Frontend (Next.js 15)

Runs at `localhost:3000` in dev / `liveo.space` in prod. Key surface areas:

- **`/discover`** — Unified creator discovery page with role, experience, and keyword filters
- **`/services`** — Browse and view service listings with tiered pricing
- **`/checkout`** — Stripe Elements checkout flow
- **`/orders`** — Buyer and seller order management views
- **`/messages`** — Direct conversation UI between users
- **`/dashboard`** — Seller earnings, Stripe Connect status, order overview
- **`/notifications`** — In-app notification center with unread badge
- **`/profile`** — User profile with portfolio, skills, bio, role

See [[Docs/design/PROJECT_STRUCTURE]] for full directory layout.

### 2. Backend (Rails 8 API)

Runs at `localhost:4000` in dev. Exposes a REST API consumed by the Next.js frontend.

Key controllers / resources:
- **Users / Auth** — JWT issuance, Auth0 callback handling
- **Services + Tiers** — CRUD for service listings with nested `ServiceTier` records (JSONB features)
- **Orders** — Full order lifecycle state machine
- **Conversations / Messages** — Direct messaging
- **Notifications** — In-app notification model (12 event types)
- **Stripe** — PaymentIntent creation, webhook handling, Connect onboarding, payout requests
- **Subscribers** — Newsletter sign-up (double opt-in)

See [[Docs/api/API_OVERVIEW]] for endpoint reference.

### 3. Authentication

Auth0 handles OAuth flows (Google, GitHub). The backend issues **24-hour JWTs** on successful auth. The frontend stores the token and sends it as a Bearer header on all API requests.

See [[Docs/api/AUTH0_SETUP]] for configuration details.

### 4. Payments (Stripe)

Two-sided payment flow:
- **Buyers** pay via Stripe Elements (`PaymentIntent`)
- **Sellers** receive payouts via **Stripe Connect** (14-day hold, then `Transfer`)
- **Webhooks** handle async events: `payment_intent.succeeded`, `payment_intent.failed`, `payment_intent.canceled`

See [[Docs/services/STRIPE_INTEGRATION]] for full setup.

### 5. Orders & Delivery

Orders follow a strict lifecycle state machine:

```
pending → paid → in_progress → in_review → completed
                                    ↑
                              (revision loop)
```

Buyers can request revisions (with seller-defined limits). Deliverables are uploaded/downloaded via Active Storage.

See [[Docs/services/SERVICES_WORKFLOW_ENABLEMENT_PLAN]] and [[Docs/services/SERVICES_WORKFLOW_IMPLEMENTATION_GUIDE]].

### 6. Email & Notifications

All key events (order updates, messages, earnings, payouts) trigger:
1. An **in-app notification** (stored in DB, surfaced in notification bell)
2. An **email** via Resend (queued through `SendNotificationEmailJob` on SolidQueue)

12 notification event types are handled by `NotificationService` — a single unified entry point.

See [[Docs/email/EMAIL_NOTIFICATION_STATUS]] (current state) and [[Docs/email/EMAIL_SYSTEM_PLAN]] (architecture).

### 7. Messaging

Direct user-to-user conversations. Messages are displayed in real-time (polling or subscription). Read status is tracked per message.

A planned v2 ([[Docs/messaging/MESSAGING_ENHANCEMENT_PLAN]]) will add file sharing, service offers, and order initiation from within the chat thread.

### 8. Deployment & CI/CD

- **Docker Compose** for local dev (frontend + backend + DB containers)
- **GitHub Actions** runs CI on PRs: lint, type check, build (frontend); Rails tests (backend)
- **Fly.io** auto-deploys on pushes to `main`
- Required secrets: `FLY_API_TOKEN`, `NEXT_PUBLIC_AUTH0_DOMAIN`, `NEXT_PUBLIC_AUTH0_CLIENT_ID`

See [[Docs/deployment/DEPLOYMENT_SETUP]].

---

## Domain Model (14 Entities)

Per [[Docs/design/SYSTEM_ONTOLOGY]]:

| Entity | Description |
|---|---|
| User | Core identity; has role (Producer, Vocalist, Engineer) |
| Profile | Bio, skills, experience level, avatar |
| Portfolio / PortfolioItem | Showcase work with audio previews |
| Service | A service listing owned by a seller |
| ServiceTier | Basic / Standard / Premium tiers with JSONB features |
| Order | Ties a buyer to a service tier; drives the lifecycle state machine |
| OrderRevision | Revision request/response attached to an order |
| Conversation | Thread between two users |
| Message | Individual message in a conversation |
| Notification | In-app notification (12 event types) |
| Subscriber | Newsletter subscriber (double opt-in) |
| StripeAccount | Seller's Stripe Connect account record |
| Payout | Payout request tied to a StripeAccount |

---

## How the Components Connect

```
[Browser / Next.js 15]
        │  REST (Bearer JWT)
        ▼
[Rails 8 API — port 4000]
        │
        ├──▶ [PostgreSQL] — all persistent data
        │
        ├──▶ [Auth0]       — OAuth flows, JWT validation
        │
        ├──▶ [Stripe]      — PaymentIntent, Connect, webhooks
        │
        ├──▶ [Resend]      — transactional email delivery
        │
        ├──▶ [SolidQueue]  — async job queue (email jobs)
        │
        └──▶ [Active Storage] — file uploads (deliverables, portfolio)

[GitHub Actions CI/CD]
        └──▶ [Fly.io]      — production deployment
```

---

## Platform Phase Status

| Phase | Scope | Status |
|---|---|---|
| Phase 1 | Auth, Discovery, Services, Payments, Orders, Messaging, Seller Dashboard | ✅ Complete |
| Phase 2 | Email & Notifications (Resend, 12 event types, newsletter) | ✅ Complete |
| Phase 3 | Tech Debt (hardcoded data, order scoping, auth persistence, lint) | 🔧 Next |
| Phase 4 | Admin Hub (user mgmt, error monitoring, metrics) | 📋 Planned |
| Phase 5 | Support System (tickets, FAQ, admin response) | 📋 Planned |
| Phase 6a | Reviews & Ratings (real review model replacing hardcoded data) | 📋 Planned |
| Phase 6b | Service-Oriented Messaging v2 (file sharing, offers, order initiation) | 📋 Planned |
| Phase 7 | Polish & Scale (testing, rate limiting, mobile audit) | 🔮 Future |

See [[Docs/PLATFORM_ROADMAP]] for full details.

---

## Related Notes

- [[Docs/design/SYSTEM_ONTOLOGY]] — Complete domain model and state machines
- [[Docs/design/PROJECT_SUMMARY]] — High-level project overview
- [[Docs/api/API_OVERVIEW]] — REST endpoint reference
- [[Docs/services/SERVICES_KNOWN_ISSUES]] — Current tech debt tracker
- [[_System Map/Components]] — Component breakdown
- [[_System Map/Decisions]] — Architecture decision log
