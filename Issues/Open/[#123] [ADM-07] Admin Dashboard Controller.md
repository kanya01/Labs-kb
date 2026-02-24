---
title: "[ADM-07] Admin Dashboard Controller"
type: issue
status: open
linked-repo: kanya01/COLABS
linked-pr: ""
linked-issue: https://github.com/kanya01/COLABS/issues/123
tags: [backend, priority-critical, dashboard, admin, metrics]
updated: 2026-02-24
---

# [ADM-07] Admin Dashboard Controller

> **Priority**: P0 — Critical | **Phase**: 2 — Backend Controllers | **Effort**: 3–4 hours

## Task
1. Create `Api::V1::Admin::DashboardController` inheriting from `Admin::BaseController`
2. `#index` — aggregate metrics across all platform tables (users, orders, earnings, payouts, newsletter, errors, audit logs)
3. `#metrics` — time-series data for trend charts (accepts `period` param: 7d, 30d, 90d)
4. Include Solid Queue job monitoring (failed, pending, scheduled counts + recent failures)

## Acceptance Criteria
- [ ] `GET /api/v1/admin/dashboard` returns complete metrics JSON
- [ ] Metrics include: users (total, new, by_role, verified, banned), orders (total, active, completed, GMV), earnings (fees, pending payouts, paid), newsletter (total, confirmed), errors (unacknowledged, last_24h), recent admin activity
- [ ] `GET /api/v1/admin/dashboard/metrics?period=30d` returns time-series data
- [ ] All database queries are efficient (no N+1)

## Dependencies
- **Blocked By**: [[open#119] [ADM-03] Admin Routes and Base Controller]]
- **Blocks**: #FE-02 ([[open#131] [FE-02] Admin Dashboard Page]])

## Related
- [[Docs/admin/ADMIN_HUB_PLAN]]
- [[open#76] Admin hub]]
