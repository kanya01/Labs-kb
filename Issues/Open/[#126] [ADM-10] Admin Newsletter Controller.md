---
title: "[ADM-10] Admin Newsletter Controller"
type: issue
status: open
linked-repo: kanya01/COLABS
linked-pr: ""
linked-issue: https://github.com/kanya01/COLABS/issues/126
tags: [backend, admin, newsletter]
updated: 2026-02-24
---

# [ADM-10] Admin Newsletter Controller

> **Priority**: P2 — Medium | **Phase**: 2 — Backend Controllers | **Effort**: 2–3 hours

## Task
1. Create `Api::V1::Admin::NewsletterController` inheriting from `Admin::BaseController`
2. `#index` — list all subscribers with status filter (active, unsubscribed, etc.)
3. `#stats` — counts by status, recent subscriptions trend
4. `#broadcast` — (future: compose and send newsletter to all confirmed subscribers)

## Acceptance Criteria
- [ ] `GET /admin/newsletter` returns all subscribers
- [ ] `GET /admin/newsletter/stats` returns aggregate counts
- [ ] Subscriber data includes: email, status, confirmed_at, source, created_at

## Dependencies
- **Blocked By**: [[open#119] [ADM-03] Admin Routes and Base Controller]]
- **Blocks**: #FE-05 ([[open#134] [FE-05] Admin Newsletter Page]])

## Related
- [[Docs/admin/ADMIN_HUB_PLAN]]
- [[Docs/email/EMAIL_NOTIFICATION_STATUS]]
- [[open#76] Admin hub]]
