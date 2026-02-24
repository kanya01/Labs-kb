---
title: "[FE-04] Admin Orders Page"
type: issue
status: open
linked-repo: kanya01/COLABS
linked-pr: ""
linked-issue: https://github.com/kanya01/COLABS/issues/133
tags: [orders, frontend, priority-high, admin]
updated: 2026-02-24
---

# [FE-04] Admin Orders Page

> **Priority**: P1 — High | **Phase**: 3 — Frontend | **Effort**: 5–6 hours

## Task
1. Create `src/app/admin/orders/page.tsx` — order list with filter by status, sort, pagination
2. Display: order ID, buyer/seller names, service title, amount, status, created_at
3. Force-cancel action with reason input and confirmation dialog
4. Link to buyer/seller user detail pages

## Acceptance Criteria
- [ ] Order list shows all platform orders
- [ ] Filters by status work correctly
- [ ] Force-cancel works and updates UI
- [ ] Order detail shows buyer, seller, service, and timeline

## Dependencies
- **Blocked By**: [[open#130] [FE-01] Admin Layout and Auth Guard]], [[open#125] [ADM-09] Admin Orders Controller]]
- **Blocks**: None

## Related
- [[Docs/admin/ADMIN_HUB_PLAN]]
- [[Docs/services/SERVICES_WORKFLOW_ENABLEMENT_PLAN]]
- [[open#76] Admin hub]]
