---
title: "[ADM-09] Admin Orders Controller"
type: issue
status: open
linked-repo: kanya01/COLABS
linked-pr: ""
linked-issue: https://github.com/kanya01/COLABS/issues/125
tags: [backend, orders, priority-high, admin]
updated: 2026-02-24
---

# [ADM-09] Admin Orders Controller

> **Priority**: P1 — High | **Phase**: 2 — Backend Controllers | **Effort**: 3–4 hours

## Task
1. Create `Api::V1::Admin::OrdersController` inheriting from `Admin::BaseController`
2. `#index` — list all orders with filter by status, pagination, sort by created_at
3. `#show` — full order detail including buyer, seller, service, tier, deliverables, revisions
4. `#force_cancel` — cancel any order via `OrderService.cancel_order(reason:, actor:)`, log admin action
5. Add `actor:` parameter support to `OrderService#cancel_order` (backward-compatible)

## Acceptance Criteria
- [ ] `GET /admin/orders` returns all platform orders (not scoped to current user)
- [ ] `GET /admin/orders?status=in_progress` returns filtered orders
- [ ] `POST /admin/orders/:id/force_cancel` transitions order to cancelled via OrderService
- [ ] Force-cancel sends notifications to buyer and seller
- [ ] Force-cancel creates audit log entry
- [ ] Cannot force-cancel already-completed or already-cancelled orders

## Dependencies
- **Blocked By**: [[open#119] [ADM-03] Admin Routes and Base Controller]], [[open#120] [ADM-04] Audit Log Model and Service]]
- **Blocks**: #FE-04 ([[open#133] [FE-04] Admin Orders Page]])

## Related
- [[Docs/admin/ADMIN_HUB_PLAN]]
- [[Docs/services/SERVICES_WORKFLOW_ENABLEMENT_PLAN]]
- [[open#76] Admin hub]]
