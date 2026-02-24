---
title: Platform Roadmap — live.o
type: doc
status: current
linked-repo: https://github.com/kanya01/COLABS
linked-pr: ""
linked-issue: ""
tags: [roadmap, planning, live-o]
updated: 2026-02-20
---

# Platform Roadmap — live.o

> Source: [docs/PLATFORM_ROADMAP.md](https://github.com/kanya01/COLABS/blob/main/docs/PLATFORM_ROADMAP.md)
> Last updated in repo: 2026-02-18

Full roadmap for the live.o music collaboration marketplace.

---

## Phase Status Summary

| Phase    | Scope                      | Duration  | Status     |
| -------- | -------------------------- | --------- | ---------- |
| Phase 1  | Core Platform              | —         | ✅ Complete |
| Phase 2  | Email & Notifications      | —         | ✅ Complete |
| Phase 3  | Tech Debt Resolution       | 2–3 weeks | 🔧 Next    |
| Phase 4  | Admin Hub                  | 3–4 weeks | 📋 Planned |
| Phase 5  | Support System             | 2–3 weeks | 📋 Planned |
| Phase 6a | Reviews & Ratings          | 2–3 weeks | 📋 Planned |
| Phase 6b | Service-Oriented Messaging | 4–6 weeks | 📋 Planned |
| Phase 7  | Polish & Scale             | Ongoing   | 🔮 Future  |

---

## ✅ Phase 1 — Core Platform (Complete)

Auth, discovery, services/tiers, Stripe payments, orders & delivery, messaging, seller dashboard. All running on Fly.io at `liveo.space`.

## ✅ Phase 2 — Email & Notifications (Complete)

All 12 issues from the email plan implemented. Resend delivery, branded templates, newsletter (double opt-in), in-app notifications (12 event types), `NotificationService`, `SendNotificationEmailJob` (SolidQueue), notification bell, full notification center at `/notifications`.

See [[Docs/email/EMAIL_NOTIFICATION_STATUS]].

## 🔧 Phase 3 — Tech Debt (Next)

Four issues to resolve before adding features. See [[Docs/services/SERVICES_KNOWN_ISSUES]]:
- **3.1** ~~Hardcoded service data in frontend → replace with dynamic API fetching (P1, 2–3 days)~~
	- Resolved
- **3.2** ~~Order & sell scoping — ensure buyer/seller isolation, prevent self-purchase (P1, 2–3 days)~~
	- Resolved
- **3.3** Auth persistence — token refresh, cross-tab sync, session recovery (P2, 3–5 days)
	- Investigating
- **3.4** ~~Lint & type check failures — fix ESLint violations, TypeScript errors; make CI blocking (P1, 2–3 days)~~
	- ~~Need to categorise by priority and address in chunks so as to not affect functionality~~


## 📋 Phase 4 — Admin Hub (Planned, 3–4 weeks)

Private authenticated admin panel: error monitoring, user management, sign-up monitoring, support queries, newsletter broadcasts, platform metrics. See [[Docs/admin/ADMIN_HUB_PLAN]].

## 📋 Phase 5 — Support System (Planned, 2–3 weeks)

User-facing help flow: support ticket model (open → in_progress → resolved), admin response interface, email notifications on ticket updates, FAQ/knowledge base. See [[Docs/admin/SUPPORT_SYSTEM_PLAN]].

## 📋 Phase 6a — Reviews & Ratings (Planned, 2–3 weeks)

Replace hardcoded `rating` / `reviewsCount` with real review model tied to completed orders. Star ratings (1–5), seller responses, aggregate computation. See [[Docs/services/REVIEWS_SYSTEM_PLAN]].

## 📋 Phase 6b — Service-Oriented Messaging (Planned, 4–6 weeks)

Transform messaging into a collaboration hub: file sharing, service offers, order initiation from chat, order status badges in thread, rich message types, read receipts. See [[Docs/messaging/MESSAGING_ENHANCEMENT_PLAN]].

## 🔮 Phase 7 — Polish & Scale (Future)

Frontend polish (audio waveform, infinite scroll, mobile audit), backend hardening (90%+ test coverage, rate limiting, OpenAPI spec, N+1 elimination), email preference center, push notifications, advanced search, analytics dashboard for sellers.

---

See also: [[_System Map/Architecture]] · [[Docs/INDEX]]
