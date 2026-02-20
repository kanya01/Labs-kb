# System Dashboard

> Last synced: 2026-02-20

---

## 🔴 Open Issues
```dataview
TABLE status, linked-issue, linked-repo, tags
FROM "Issues/Open"
SORT file.mtime DESC
```

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
