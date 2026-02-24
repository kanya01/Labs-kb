
---
title: Components — live.o System Map
type: system-map
status: current
linked-repo: https://github.com/kanya01/COLABS
linked-pr: ""
linked-issue: ""
tags: [components, system-map, architecture, live-o]
updated: 2026-02-21
---

# Components — live.o System Map

> Every major module across the frontend, backend, service layer, domain models, jobs, mailers, and external integrations.
> Cross-referenced with doc notes and open issues.

See also: [[_System Map/Architecture]] · [[_System Map/Decisions]] · [[Docs/design/SYSTEM_ONTOLOGY]] · [[Docs/design/PROJECT_STRUCTURE]]

---

## 1. Frontend — Next.js 15

Stack: **Next.js 15 · React 19 · TypeScript · Tailwind CSS · Framer Motion · Zustand · React Query**

### 1.1 Pages & Routes

| Route | Component / Purpose |
|---|---|
| `/discover` | Unified creator discovery — role, experience, keyword filters; user cards with portfolio audio preview |
| `/services/:id` | Service detail page — description, tier comparison table (Basic / Standard / Premium) |
| `/checkout` | Stripe Elements payment form — renders on order creation, collects card details |
| `/orders` | Order list — buyer sees purchases, seller sees sales, filtered by `?role=buyer\|seller` |
| `/orders/:id` | Order detail — status badge, deliverables list, revision thread, action buttons |
| `/messages` | Conversation list and active chat thread |
| `/dashboard` | Seller dashboard — earnings tiles, order management, Stripe Connect status |
| `/notifications` | Full notification center; individual items deep-link via `action_url` |
| `/profile/:id` | User profile — bio, skills, role, portfolio items with audio player |
| `/auth/callback` | Auth0 OAuth return URL — exchanges code for JWT |

**Issues touching frontend:**
- [[open#54] Fix failing lint & type checks]] — ESLint violations and TypeScript errors across all pages
- [[open#55] Implement testing strategy for front end typescript components]] — unit + E2E coverage plan

**Docs:** [[Docs/design/PROJECT_STRUCTURE]] · [[Docs/design/DESIGN_AND_ROADMAP]] · [[Docs/design/STYLES_AND_CONVENTIONS]]

---

### 1.2 State Management

| Layer | Library | Responsibility |
|---|---|---|
| **Client state** | Zustand | Auth token, user identity, UI toggles (notification bell open, modal state) |
| **Server state** | React Query | API data fetching, caching, background refetching, request deduplication |
| **Form state** | Native React / uncontrolled | Checkout form (delegated to Stripe Elements); other forms use controlled components |

---

### 1.3 API Client (`/src/lib/api/`)

Centralised HTTP layer for all backend requests. Responsibilities:

- Attaches `Authorization: Bearer <token>` header on every protected request
- Wraps `fetch` or `axios` with base URL (`NEXT_PUBLIC_API_URL`)
- Surfaces typed error responses for React Query consumers
- Handles 401 responses (token expiry → logout / refresh)

**Issues:** [[open#54] Fix failing lint & type checks]] (type errors in client layer)

---

### 1.4 Stripe Elements (Checkout)

Renders Stripe's hosted card input inside the checkout page. Receives `client_secret` from the backend `POST /orders/:id/payments/create_intent` endpoint and calls `stripe.confirmPayment()` on submit. No card data ever touches the Rails server.

**Docs:** [[Docs/services/STRIPE_INTEGRATION]] · [[Docs/services/BUYER_GUIDE]]

---

### 1.5 Notification Bell

Header component that polls `/notifications` (or receives push). Shows unread count badge. Clicking opens a popover of recent notifications; each item navigates to its `action_url`. Full list at `/notifications`.

**Docs:** [[Docs/email/EMAIL_NOTIFICATION_STATUS]]

---

## 2. Backend — Rails 8 API

Stack: **Ruby on Rails 8 (API mode) · PostgreSQL · Active Storage · SolidQueue**
Base URL: `http://localhost:4000/api/v1` (dev) / `https://liveo.space/api/v1` (prod)

---

### 2.1 Controllers

#### Auth (`/auth`)

| Endpoint | Method | What it does |
|---|---|---|
| `/auth/login` | POST | Email+password login → issues 24-hour JWT |
| `/auth/oauth/callback` | POST | Receives Auth0 token → verifies via JWKS → issues JWT |
| `/auth/me` | GET | Returns current user from JWT |

Auth0 provider/uid stored on User for social account linking.
**Docs:** [[Docs/api/AUTH0_SETUP]] · [[Docs/api/API_OVERVIEW]]

---

#### Users (`/users`)

CRUD for user accounts and profiles. `PUT /users/:id` updates bio, role, skills, experience level. Avatar uploaded as multipart form data → Active Storage.

---

#### Services + ServiceTiers (`/services`)

| Action | Notes |
|---|---|
| `GET /services` | Public listing of all active services |
| `POST /services` | Create service with nested `service_tiers_attributes` (up to 3 tiers) |
| `PUT /services/:id` | Update service and nested tiers atomically |
| `DELETE /services/:id` | Owner only |

Accepts nested attributes so a service and all its tiers can be created/updated in one request.
**Docs:** [[Docs/services/SERVICES_WORKFLOW_ENABLEMENT_PLAN]] · [[Docs/api/API_OVERVIEW]]

---

#### Orders (`/orders`)

Core lifecycle controller. Filterable by `role=buyer|seller` and `status`.

| Action | Auth Rule |
|---|---|
| `POST /orders` | Any authenticated user (becomes buyer) |
| `PUT /orders/:id` — to `in_progress`, `in_review` | Seller only |
| `PUT /orders/:id` — to `completed`, `revision_requested` | Buyer only |
| `DELETE /orders/:id` | Buyer (pending/paid) or Seller (pending/paid/in_progress) |

State transitions validated by `OrderService`. See state machine in [[_System Map/Architecture]].
**Docs:** [[Docs/services/SERVICES_WORKFLOW_IMPLEMENTATION_GUIDE]] · [[Docs/services/BUYER_GUIDE]] · [[Docs/services/SELLER_GUIDE]]
**Issues:** [[open#21] Comprehensive Backend Testing for Services Workflow]] · [[open#22] End-to-End Integration Tests for Critical Workflows]]

---

#### OrderRevisions (`/orders/:id/revisions`)

| Action | Auth Rule |
|---|---|
| `POST` — request revision | Buyer only; order must be `in_review`; enforces `service_tier.revision_count` limit |
| `PUT /:revision_id` — respond | Seller only; can set `start_revision: true` to move order back to `in_progress` |

Returns `revisions_used`, `revisions_limit`, `revisions_remaining` on list.
**Issues:** [[open#21] Comprehensive Backend Testing for Services Workflow]]

---

#### OrderDeliverables (`/orders/:id/deliverables`)

| Action | Auth Rule |
|---|---|
| `POST` | Seller only; order must be paid, in_progress, in_review, or revision_requested |
| `GET /:id/download` | Buyer or seller; returns signed Active Storage URL |
| `DELETE /:id` | Seller only; cannot delete from completed orders |

**Docs:** [[Docs/services/FILE_UPLOAD_GUIDE]]

---

#### Payments (`/orders/:id/payments`)

| Endpoint | What it does |
|---|---|
| `POST /create_intent` | Creates Stripe `PaymentIntent`; returns `client_secret` to frontend |
| `POST /confirm` | Confirms payment with `payment_method_id` |
| `GET /status` | Returns current PaymentIntent status |

**Docs:** [[Docs/services/STRIPE_INTEGRATION]]
**Issues:** [[open#25] Security Audit for Payment and Payout Systems]]

---

#### Webhooks (`/webhooks/stripe`)

Single endpoint handling all Stripe events. Validates signature using `STRIPE_WEBHOOK_SECRET` before processing.

| Event | Handler |
|---|---|
| `payment_intent.succeeded` | Updates order to `paid`, creates Earning |
| `payment_intent.payment_failed` | Logs failure |
| `payment_intent.canceled` | Logs cancellation |
| `account.updated` | `StripeConnectService` — updates SellerProfile status |
| `account.application.authorized/deauthorized` | `StripeConnectService` |
| `transfer.created/updated/failed/reversed` | `PayoutService` — updates Payout record |

**Issues:** [[open#25] Security Audit for Payment and Payout Systems]] · [[open#22] End-to-End Integration Tests for Critical Workflows]]

---

#### Stripe Connect (`/stripe_connect`)

| Endpoint | What it does |
|---|---|
| `POST /create_account` | Creates Stripe Express account; saves `account_id` on SellerProfile |
| `GET /onboarding_link` | Generates Stripe onboarding URL for seller to submit details |
| `GET /account_status` | Returns `details_submitted`, `charges_enabled`, `payouts_enabled` |
| `GET /dashboard_link` | Returns Stripe Express dashboard login URL |

**Docs:** [[Docs/services/STRIPE_INTEGRATION]] · [[Docs/services/SELLER_GUIDE]]
**Issues:** [[open#25] Security Audit for Payment and Payout Systems]] · [[open#26] Production Configuration and Deployment Setup]]

---

#### Seller Dashboard (`/seller/dashboard`, `/seller/earnings`, `/seller/payouts`)

| Endpoint | Response |
|---|---|
| `GET /dashboard/stats` | `total_earnings`, `pending_earnings`, `available_balance`, `active_orders_count`, `completed_orders_count` |
| `GET /earnings` | Paginated list of Earning records with order details |
| `GET /payouts` | Paginated payout history |
| `POST /payouts` | Request payout for `amount`; deducts from available balance via Stripe Transfer |
| `GET /payouts/balance` | `{ available, pending }` |

**Issues:** [[open#76] Admin hub]] (admin view of platform-wide equivalents)

---

#### Conversations + Messages (`/conversations`, `/conversations/:id/messages`)

Direct user-to-user messaging. Creating a conversation requires `recipient_id`. Messages are simple `body` + `read` boolean; read status is tracked per message.

**Docs:** [[Docs/messaging/MESSAGING_ENHANCEMENT_PLAN]] (v2 planned with file sharing + service offers)

---

#### Notifications (`/notifications`)

| Endpoint | What it does |
|---|---|
| `GET /notifications` | Returns recent notifications for current user (unread first) |
| `PUT /notifications/:id/read` | Marks single notification as read |
| `PUT /notifications/read_all` | Marks all as read |

**Docs:** [[Docs/email/EMAIL_NOTIFICATION_STATUS]]

---

#### Newsletter Subscribers (`/subscribers`)

| Endpoint | What it does |
|---|---|
| `POST /subscribers` | Creates subscriber record + sends confirmation email via Resend |
| `GET /subscribers/confirm?token=` | Confirms subscription (double opt-in) |
| `DELETE /subscribers/unsubscribe?token=` | Unsubscribes |

**Docs:** [[Docs/email/EMAIL_SYSTEM_PLAN]]

---

## 3. Service Layer (`backend/app/services/`)

The business logic layer — controllers stay thin by delegating to these.

---

### 3.1 OrderService

**File**: `app/services/order_service.rb`

The central orchestrator for the order lifecycle.

| Method | What it does |
|---|---|
| `create_order(buyer:, service_tier:, requirements:)` | Validates buyer ≠ seller, creates Order in `pending` state |
| `transition_status(new_status)` | Validates transition is permitted (see map below), fires callbacks |
| `start_progress()` | `paid → in_progress` (seller action) |
| `submit_for_review()` | `in_progress → in_review` (seller action) |
| `request_revision(feedback:)` | `in_review → revision_requested` (buyer action); checks revision limit |
| `complete_order()` | `in_review → completed` (buyer action); triggers Earning creation |
| `cancel_order(reason:)` | Cancels from any non-final state |
| `allowed_transitions()` | Returns array of valid next statuses for current actor |

**Valid transition map:**

| From | Allowed to |
|---|---|
| `pending` | `paid`, `cancelled` |
| `paid` | `in_progress`, `cancelled` |
| `in_progress` | `in_review`, `cancelled` |
| `in_review` | `revision_requested`, `completed` |
| `revision_requested` | `in_progress`, `cancelled` |

**Docs:** [[Docs/services/SERVICES_WORKFLOW_ENABLEMENT_PLAN]] · [[Docs/design/SYSTEM_ONTOLOGY]]
**Issues:** [[open#21] Comprehensive Backend Testing for Services Workflow]] · [[open#22] End-to-End Integration Tests for Critical Workflows]]

---

### 3.2 PaymentService

**File**: `app/services/payment_service.rb`

Wraps all Stripe PaymentIntent interactions.

| Method | What it does |
|---|---|
| `create_payment_intent()` | Creates `Stripe::PaymentIntent` for the order amount; stores `stripe_payment_intent_id` |
| `confirm_payment(payment_method_id)` | Confirms intent; Stripe fires webhook on success |
| `retrieve_payment_intent()` | Fetches current intent status from Stripe |
| `process_successful_payment()` | Called by webhook handler — transitions order to `paid` |

**Docs:** [[Docs/services/STRIPE_INTEGRATION]]
**Issues:** [[open#25] Security Audit for Payment and Payout Systems]]

---

### 3.3 EarningsService

**File**: `app/services/earnings_service.rb`

Manages seller revenue tracking and the 14-day hold period.

| Method | What it does |
|---|---|
| `create_earning()` | Creates Earning record (`gross - 10% fee = net`); sets `available_at = now + 14 days` |
| `.available_balance(seller)` | Sum of `available` earnings for a seller |
| `.pending_balance(seller)` | Sum of `pending` earnings still in hold |
| `.earnings_for_payout(seller)` | Returns `available` earnings ready to transfer |
| `.mark_as_paid_out(earning_ids)` | Batch-transitions earnings to `paid_out` after transfer |

**Platform fee**: 10% (configurable via `PLATFORM_FEE_PERCENTAGE` env var)

**Docs:** [[Docs/services/SELLER_GUIDE]] · [[Docs/design/SYSTEM_ONTOLOGY]]

---

### 3.4 PayoutService

**File**: `app/services/payout_service.rb`

Handles payout creation via Stripe Transfer and webhook reconciliation.

| Method | What it does |
|---|---|
| `balance()` | Returns `{ available, pending, total }` for the seller |
| `create_payout(amount)` | Validates amount ≤ available balance; creates `Stripe::Transfer` to connected account |
| `payout_history()` | Recent paginated payouts |
| Webhook: `handle_transfer_created` | Creates or updates Payout record to `in_transit` |
| Webhook: `handle_transfer_updated` | Updates status on change |
| Webhook: `handle_transfer_failed` | Marks payout `failed`, fires notification |
| Webhook: `handle_transfer_reversed` | Handles reversal |

**Docs:** [[Docs/services/STRIPE_INTEGRATION]]
**Issues:** [[open#25] Security Audit for Payment and Payout Systems]] · [[open#26] Production Configuration and Deployment Setup]]

---

### 3.5 StripeConnectService

**File**: `app/services/stripe_connect_service.rb`

Manages seller Stripe Express account lifecycle.

| Method | What it does |
|---|---|
| `create_account()` | Creates `Stripe::Account` (Express type); saves `stripe_connect_account_id` on SellerProfile |
| `create_onboarding_link(return_url, refresh_url)` | Generates one-time onboarding URL via `Stripe::AccountLink` |
| `retrieve_account_status()` | Fetches `details_submitted`, `charges_enabled`, `payouts_enabled` |
| `create_dashboard_link()` | Generates Express dashboard login link |
| Webhook: `handle_account_updated` | Syncs SellerProfile status (`verified`, `restricted`, etc.) |
| Webhook: `handle_account_authorized/deauthorized` | Updates onboarding and payout eligibility |

**Docs:** [[Docs/services/STRIPE_INTEGRATION]] · [[Docs/services/SELLER_GUIDE]]
**Issues:** [[open#26] Production Configuration and Deployment Setup]]

---

### 3.6 NotificationService

**File**: `app/services/notification_service.rb`

The single entry point for all notification creation. Keeps notification logic out of models and controllers.

| Method | What it does |
|---|---|
| `.notify(user:, type:, title:, body:, action_url:, metadata:)` | Creates `Notification` DB record + enqueues `SendNotificationEmailJob` |
| `.notify_many(users:, ...)` | Fan-out to multiple recipients with identical payload |

**12 notification types** (full list in [[Docs/email/EMAIL_NOTIFICATION_STATUS]]):
`order_created`, `payment_confirmed`, `order_in_progress`, `deliverable_uploaded`, `order_in_review`, `revision_requested`, `revision_started`, `order_completed`, `order_cancelled`, `message_received`, `earnings_available`, `payout_processed`

**Docs:** [[Docs/email/EMAIL_SYSTEM_PLAN]] · [[Docs/email/EMAIL_NOTIFICATION_STATUS]]
**Issues:** [[open#21] Comprehensive Backend Testing for Services Workflow]]

---

## 4. Domain Models (`backend/app/models/`)

All 14 entities. Full schemas, state machines, and indexes documented in [[Docs/design/SYSTEM_ONTOLOGY]].

| Model | Table | Key Relationships | Notes |
|---|---|---|---|
| **User** | `users` | `has_many` services, orders, earnings, payouts, notifications; `has_one` seller_profile | Auth via BCrypt or OAuth; `portfolio_preview` JSONB cached for cards |
| **Service** | `services` | `belongs_to` user; `has_many` service_tiers, orders | `price`/`delivery_time` fields are legacy — real data is in tiers |
| **ServiceTier** | `service_tiers` | `belongs_to` service; `has_many` orders | Enum: `basic=0`, `standard=1`, `premium=2`; unique per service; JSONB `features` |
| **Order** | `orders` | `belongs_to` service, service_tier, buyer (User), seller (User); `has_many` revisions, deliverables; `has_one` earning | 7-state lifecycle; `delivery_date` auto-calculated |
| **OrderRevision** | `order_revisions` | `belongs_to` order | Tracks buyer feedback + seller notes; count enforced against tier limit |
| **OrderDeliverable** | `order_deliverables` | `belongs_to` order; `has_one_attached :file` | Active Storage; signed URL for download |
| **Earning** | `earnings` | `belongs_to` seller (User), order | 3-state lifecycle; `platform_fee = 10%`; unique per order |
| **Payout** | `payouts` | `belongs_to` seller (User) | 5-state lifecycle; `stripe_payout_id` unique |
| **SellerProfile** | `seller_profiles` | `belongs_to` user (1:1) | 6-state Stripe Connect account status; unique per user |
| **PortfolioItem** | `portfolio_items` | `belongs_to` user; Active Storage `audio_file` + `cover_image` | Max 50 MB audio; signed URLs |
| **Conversation** | `conversations` | `belongs_to` sender, recipient (User); `has_many` messages | Unique constraint: one thread per user pair |
| **Message** | `messages` | `belongs_to` conversation, user | `read` boolean; future v2 adds rich types |
| **Notification** | `notifications` | `belongs_to` user | 12 types; JSONB `metadata`; `email_sent` flag; `read`/`read_at` |
| **NewsletterSubscriber** | `newsletter_subscribers` | Standalone | Double opt-in via `confirmation_token`; status: active/unsubscribed/bounced |

**Issues:** [[open#21] Comprehensive Backend Testing for Services Workflow]] (model specs for Order, ServiceTier, Earning, Payout, SellerProfile, OrderRevision, OrderDeliverable)

---

## 5. Background Jobs (`backend/app/jobs/`)

| Job | Queue | What it does |
|---|---|---|
| **SendNotificationEmailJob** | `default` | Picks up notification ID → routes to correct mailer method → sends via Resend → marks `email_sent: true`. Retries up to 3× with polynomial backoff. |
| **ReleaseEarningsJob** | `default` | Scheduled job — queries `earnings` where `status = pending` AND `available_at <= now`; batch-transitions to `available`; fires `earnings_available` notification. |

**Queue backend**: SolidQueue (Solid Queue is a DB-backed queue built into Rails 8 — no Redis required).

**Docs:** [[Docs/email/EMAIL_SYSTEM_PLAN]] · [[Docs/email/EMAIL_NOTIFICATION_STATUS]]

---

## 6. Mailers (`backend/app/mailers/`)

All mailers deliver via **Resend** (configured as the Action Mailer adapter). Each has HTML + plain-text variants. From address: `MAILER_FROM_ADDRESS` env var (`hello@liveo.space`).

| Mailer | Templates | Triggered by |
|---|---|---|
| **OrderMailer** | 16 (8 HTML + 8 text) | `SendNotificationEmailJob` on order lifecycle events: created, paid, in_progress, in_review, revision_requested, revision_started, completed, cancelled |
| **NewsletterMailer** | 4 (2 HTML + 2 text) | Direct call on subscriber creation (confirmation) and confirmation success (welcome) |
| **NotificationMailer** | 2 (1 HTML + 1 text) | `SendNotificationEmailJob` fallback for any notification type not handled by a specific mailer |

Branded design: dark theme, live.o visual language, mobile-responsive.

**Docs:** [[Docs/email/EMAIL_NOTIFICATION_STATUS]] · [[Docs/email/EMAIL_SYSTEM_PLAN]]

---

## 7. External Integrations

### 7.1 Stripe

**Purpose**: Buyer payments (PaymentIntents) + seller payouts (Connect / Transfers)

| Component | Stripe Object | Rails Handler |
|---|---|---|
| Checkout payment | `PaymentIntent` | `PaymentService`, `PaymentsController` |
| Webhook receiver | Multiple events | `WebhooksController` → delegates to services |
| Seller account | `Account` (Express) | `StripeConnectService` |
| Onboarding URL | `AccountLink` | `StripeConnectService` |
| Payout transfer | `Transfer` | `PayoutService` |
| Dashboard link | `LoginLink` | `StripeConnectService` |

**Env vars**: `STRIPE_SECRET_KEY`, `STRIPE_WEBHOOK_SECRET`, `PLATFORM_FEE_PERCENTAGE`

**Docs:** [[Docs/services/STRIPE_INTEGRATION]]
**Issues:** [[open#25] Security Audit for Payment and Payout Systems]] · [[open#26] Production Configuration and Deployment Setup]]

---

### 7.2 Auth0

**Purpose**: OAuth social login (Google, GitHub) + JWT validation

| Step | What happens |
|---|---|
| 1. User clicks "Sign in with Google" | Frontend redirects to Auth0 Universal Login |
| 2. Auth0 handles OAuth flow | Returns `id_token` + `access_token` to `/auth/oauth/callback` |
| 3. Rails validates token | Via Auth0 JWKS endpoint |
| 4. Rails issues its own JWT | 24-hour expiry, HS256 |
| 5. Frontend stores JWT | Sent as `Authorization: Bearer <token>` on all API calls |

Account linking: if an existing email matches an OAuth login, `provider` + `uid` fields on User are updated.

**Env vars**: `NEXT_PUBLIC_AUTH0_DOMAIN`, `NEXT_PUBLIC_AUTH0_CLIENT_ID`, `AUTH0_CLIENT_SECRET`, `AUTH0_AUDIENCE`

**Docs:** [[Docs/api/AUTH0_SETUP]]

---

### 7.3 Resend

**Purpose**: Transactional and newsletter email delivery

Configured as the Rails Action Mailer delivery adapter — no SMTP, API-based only (avoids port 25 blocking on Fly.io). SPF, DKIM, and DMARC configured for `liveo.space`.

| Mailer | Volume | Examples |
|---|---|---|
| Transactional | Per order event | Order paid, deliverable uploaded, revision requested |
| Newsletter | On subscriber opt-in | Confirmation link, welcome email |
| Notification fallback | Any uncovered event | Generic in-app notification email |

**Env vars**: `RESEND_API_KEY`, `MAILER_FROM_ADDRESS`, `FRONTEND_URL`

**Docs:** [[Docs/email/EMAIL_SYSTEM_PLAN]] · [[Docs/email/EMAIL_NOTIFICATION_STATUS]]

---

### 7.4 Active Storage

**Purpose**: File uploads — portfolio audio, order deliverables, user avatars

| Attachment | Model | Max Size | Allowed Types |
|---|---|---|---|
| `avatar` | User | 5 MB | JPEG, PNG, GIF, WebP |
| `audio_file` | PortfolioItem | 50 MB | MP3, WAV, OGG, AAC, FLAC |
| `cover_image` | PortfolioItem | 10 MB | JPEG, PNG, GIF, WebP |
| `file` | OrderDeliverable | 50 MB | Audio, ZIP, PDF, images |

Files are served via **signed URLs** with expiration — buyers/sellers never access storage directly. Local disk in dev; cloud storage (S3-compatible) in prod.

**Docs:** [[Docs/services/FILE_UPLOAD_GUIDE]]

---

### 7.5 SolidQueue

**Purpose**: Background job queue (ships with Rails 8, DB-backed — no Redis required)

Runs inside the Rails process (or as a separate puma worker in prod). Handles:
- `SendNotificationEmailJob` — async email dispatch
- `ReleaseEarningsJob` — scheduled 14-day hold release
- Retry logic with polynomial backoff (max 3 attempts for email jobs)

**Docs:** [[Docs/email/EMAIL_SYSTEM_PLAN]]

---

## 8. CI/CD & Deployment

### GitHub Actions

| Workflow | Trigger | Steps |
|---|---|---|
| `ci.yml` | Pull requests | Lint (ESLint) · TypeScript type check · Next.js build · RSpec (backend) |
| `fly-deploy.yml` | Push to `main` | Docker build → deploy to Fly.io |

⚠️ Lint + type checks are **not currently blocking** in CI — fixing this is tracked in [[open#54] Fix failing lint & type checks]].

### Fly.io (Production)

- Frontend and backend deployed as separate Fly apps
- PostgreSQL via Fly Postgres
- Secrets managed via `flyctl secrets set`
- `liveo.space` is the live domain

**Docs:** [[Docs/deployment/DEPLOYMENT_SETUP]]
**Issues:** [[open#57] Dockerize Development Environment]] · [[open#26] Production Configuration and Deployment Setup]]

---

## 9. Planned / In-Progress Components

These are spec'd but not yet built.

| Component | Status | Spec |
|---|---|---|
| **Admin Hub** | 📋 Planned (Phase 4) | Private panel: user mgmt, error monitoring, metrics, newsletter broadcast — [[Docs/admin/ADMIN_HUB_PLAN]] · [[open#76] Admin hub]] |
| **Support System** | 📋 Planned (Phase 5) | Help form, ticket lifecycle, admin response, FAQ — [[Docs/admin/SUPPORT_SYSTEM_PLAN]] |
| **Reviews & Ratings** | 📋 Planned (Phase 6a) | Real review model replacing hardcoded `rating`/`reviewsCount` — [[Docs/services/REVIEWS_SYSTEM_PLAN]] |
| **Messaging v2** | 📋 Planned (Phase 6b) | File sharing, service offers, order initiation from chat, rich message types — [[Docs/messaging/MESSAGING_ENHANCEMENT_PLAN]] |
| **Frontend Test Suite** | 🔧 In Progress | Jest unit + Cypress E2E — [[open#55] Implement testing strategy for front end typescript components]] · [[Docs/testing/FRONTEND_TESTING_PLAN]] |
| **Backend Test Suite** | 🔧 In Progress | RSpec model + request + integration specs — [[open#21] Comprehensive Backend Testing for Services Workflow]] · [[open#22] End-to-End Integration Tests for Critical Workflows]] |

---

## Quick Reference — Component → Doc + Issue Map

| Component | Primary Doc | Open Issues |
|---|---|---|
| Discovery page | [[Docs/discovery/DISCOVERY_FLOW_PLAN]] | — |
| Checkout / Payments | [[Docs/services/STRIPE_INTEGRATION]] | [[open#25] Security Audit for Payment and Payout Systems]] · [[open#26] Production Configuration and Deployment Setup]] |
| Order lifecycle | [[Docs/services/SERVICES_WORKFLOW_ENABLEMENT_PLAN]] | [[open#21] Comprehensive Backend Testing for Services Workflow]] · [[open#22] End-to-End Integration Tests for Critical Workflows]] |
| Notifications + Email | [[Docs/email/EMAIL_NOTIFICATION_STATUS]] | — |
| Stripe Connect (seller) | [[Docs/services/STRIPE_INTEGRATION]] | [[open#25] Security Audit for Payment and Payout Systems]] |
| Auth0 | [[Docs/api/AUTH0_SETUP]] | — |
| File uploads | [[Docs/services/FILE_UPLOAD_GUIDE]] | — |
| Deployment | [[Docs/deployment/DEPLOYMENT_SETUP]] | [[open#57] Dockerize Development Environment]] · [[open#26] Production Configuration and Deployment Setup]] |
| Frontend quality | [[Docs/testing/FRONTEND_TESTING_PLAN]] | [[open#54] Fix failing lint & type checks]] · [[open#55] Implement testing strategy for front end typescript components]] |
| Admin panel | [[Docs/admin/ADMIN_HUB_PLAN]] | [[open#76] Admin hub]] |
