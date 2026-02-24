# System Dashboard

> Last synced: 2026-02-24 · **41 open issues** · [kanya01/COLABS](https://github.com/kanya01/COLABS)
> Latest: [[Progress/2026-02-21]] — Phase 2 ✅ complete · Phase 3 🔧 in progress · Phase 4 (Admin Hub) 🆕 scoped

---

## 🔴 Open Issues (41)
```dataview
TABLE status, linked-issue, linked-repo, tags
FROM "Issues/Open"
SORT file.mtime DESC
```

### Quick Links — Open Issues

**Pre-existing (8)**
- [[open#76] Admin hub]] — `backend` `api` `dashboard` `critical`
- [[open#57] Dockerize Development Environment]] — `priority:critical` `devops`
- [[open#55] Implement testing strategy for front end typescript components]]
- [[open#54] Fix failing lint & type checks]] — `priority:critical` `frontend` `quality`
- [[open#26] Production Configuration and Deployment Setup]] — `deployment` `devops`
- [[open#25] Security Audit for Payment and Payout Systems]] — `priority:critical` `security`
- [[open#22] End-to-End Integration Tests for Critical Workflows]] — `testing` `integration`
- [[open#21] Comprehensive Backend Testing for Services Workflow]] — `backend` `testing`

**Phase 4 — Security Hardening (4)** 🆕 2026-02-24
- [[open#113] [SEC-01] Scope Public User Listing Response Fields]] — `api` `priority-critical` `security`
- [[open#114] [SEC-02] Protect Admin Fields from User Params]] — `api` `priority-critical` `security`
- [[open#115] [SEC-03] Verify JWT Expiry Enforcement]] — `security` `auth` `investigation`
- [[open#116] [SEC-04] Add Rate Limiting on Authentication Endpoints]] — `security` `priority-high`

**Phase 4 — Admin Foundation (6)** 🆕 2026-02-24
- [[open#117] [ADM-01] Database Migrations for Admin Fields]] — `database` `priority-critical` `foundation`
- [[open#118] [ADM-02] Create AdminAuthorized Concern]] — `priority-critical` `auth` `foundation`
- [[open#119] [ADM-03] Admin Routes and Base Controller]] — `priority-critical` `routing` `foundation`
- [[open#120] [ADM-04] Audit Log Model and Service]] — `priority-critical` `audit` `foundation`
- [[open#121] [ADM-05] Banned User Enforcement]] — `priority-critical` `security` `foundation`
- [[open#122] [ADM-06] Platform Error Logging Middleware]] — `priority-high` `observability`

**Phase 4 — Admin Backend Controllers (6)** 🆕 2026-02-24
- [[open#123] [ADM-07] Admin Dashboard Controller]] — `backend` `priority-critical` `metrics`
- [[open#124] [ADM-08] Admin Users Controller]] — `backend` `priority-critical` `users`
- [[open#125] [ADM-09] Admin Orders Controller]] — `backend` `priority-high` `orders`
- [[open#126] [ADM-10] Admin Newsletter Controller]] — `backend` `newsletter`
- [[open#127] [ADM-11] Admin Errors Controller]] — `backend` `priority-high` `observability`
- [[open#128] [ADM-12] Admin Audit Logs Controller]] — `backend` `priority-high` `audit`

**Phase 4 — Admin Frontend (8)** 🆕 2026-02-24
- [[open#129] [FE-08] Admin API Service and Type Updates]] — `priority-critical` `types` `foundation`
- [[open#130] [FE-01] Admin Layout and Auth Guard]] — `priority-critical` `layout` `foundation`
- [[open#131] [FE-02] Admin Dashboard Page]] — `priority-critical` `dashboard`
- [[open#132] [FE-03] Admin User Management Page]] — `priority-critical` `users`
- [[open#133] [FE-04] Admin Orders Page]] — `priority-high` `orders`
- [[open#134] [FE-05] Admin Newsletter Page]] — `newsletter`
- [[open#135] [FE-06] Admin Errors Page]] — `priority-high` `observability`
- [[open#136] [FE-07] Admin Audit Log Page]] — `priority-high` `audit`

**Phase 4 — Admin Testing (3)** 🆕 2026-02-24
- [[open#137] [TEST-01] Admin Security Integration Tests]] — `priority-critical` `security`
- [[open#138] [TEST-02] Admin Controller Unit Tests]] — `priority-high` `controllers`
- [[open#139] [TEST-03] Admin Model Unit Tests]] — `priority-high` `models`

**Future / Planned (6)** 🆕 2026-02-24
- [[open#140] [FUTURE-01] Support Ticket Admin View]] — `priority-high` `future`
- [[open#141] [FUTURE-02] Two-Factor Authentication for Admin Accounts]] — `security` `future`
- [[open#142] [FUTURE-03] Granular Admin Role System]] — `auth` `future`
- [[open#143] [FUTURE-04] Sentry Integration for Error Monitoring]] — `infrastructure` `future`
- [[open#144] [FUTURE-05] Content Moderation Tooling]] — `future`
- [[open#145] [FUTURE-06] Exportable Analytics & Reports]] — `analytics` `future`

---

## 📄 Docs — In Progress
```dataview
TABLE status, updated, linked-repo
FROM "Docs"
WHERE status = "in-progress"
SORT updated DESC
```

---

## ✅ Recently Closed
```dataview
TABLE status, linked-issue
FROM "Issues/Closed"
SORT file.mtime DESC
LIMIT 10
```

---

## 📅 Progress Log
```dataview
LIST
FROM "Progress"
SORT file.name DESC
LIMIT 14
```

---

## 🗺️ System Map
- [[_System Map/Architecture]]
- [[_System Map/Components]]
- [[_System Map/Decisions]]

---

## 📚 Docs — live.o (kanya01/COLABS)

> Last synced from GitHub: 2026-02-20

### Design & Architecture
- [[Docs/INDEX]] — Master documentation index
- [[Docs/PLATFORM_ROADMAP]] — Phase status and upcoming work
- [[Docs/design/SYSTEM_ONTOLOGY]] — 14-entity domain model, state machines
- [[Docs/design/PROJECT_SUMMARY]] — High-level platform overview
- [[Docs/design/PROJECT_STRUCTURE]] — Monorepo layout
- [[Docs/design/DESIGN_AND_ROADMAP]] — UI/UX principles
- [[Docs/design/STYLES_AND_CONVENTIONS]] — CSS tokens and conventions

### API & Auth
- [[Docs/api/API_OVERVIEW]] — REST endpoint reference
- [[Docs/api/AUTH0_SETUP]] — OAuth configuration

### Services & Payments
- [[Docs/services/SERVICES_WORKFLOW_ENABLEMENT_PLAN]] — Full workflow architecture
- [[Docs/services/SERVICES_WORKFLOW_IMPLEMENTATION_GUIDE]] — Build reference
- [[Docs/services/SERVICES_WORKFLOW_IMPLEMENTATION_ISSUES]] — 20 GitHub issue specs
- [[Docs/services/SERVICES_KNOWN_ISSUES]] — ⚠️ Active tech debt (Phase 3)
- [[Docs/services/STRIPE_INTEGRATION]] — Payments & Connect
- [[Docs/services/REVIEWS_SYSTEM_PLAN]] — Planned: Reviews & ratings
- [[Docs/services/BUYER_GUIDE]] — Buyer user guide
- [[Docs/services/SELLER_GUIDE]] — Seller user guide
- [[Docs/services/FILE_UPLOAD_GUIDE]] — Active Storage file handling

### Email & Notifications
- [[Docs/email/EMAIL_NOTIFICATION_STATUS]] — ✅ Current state (all implemented)
- [[Docs/email/EMAIL_SYSTEM_PLAN]] — Architecture plan
- [[Docs/email/EMAIL_SYSTEM_ISSUES]] — 12 GitHub issue specs

### Admin & Support (Planned)
- [[Docs/admin/ADMIN_HUB_PLAN]] — Admin panel specification
- [[Docs/admin/SUPPORT_SYSTEM_PLAN]] — Help desk specification

### Messaging
- [[Docs/messaging/MESSAGING_ENHANCEMENT_PLAN]] — Planned: messaging v2

### Discovery
- [[Docs/discovery/DISCOVERY_FLOW_PLAN]] — Discover page design
- [[Docs/discovery/DISCOVERY_FLOW_ISSUES]] — GitHub issue specs

### Testing
- [[Docs/testing/TESTING_GUIDE]] — How to run tests
- [[Docs/testing/TESTING_STRATEGY]] — Coverage goals
- [[Docs/testing/FRONTEND_TESTING_PLAN]] — Cypress & Jest plan

### Deployment
- [[Docs/deployment/DEPLOYMENT_SETUP]] — Fly.io, Docker, CI/CD
