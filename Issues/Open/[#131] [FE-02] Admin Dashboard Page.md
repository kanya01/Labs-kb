---
title: "[FE-02] Admin Dashboard Page"
type: issue
status: open
linked-repo: kanya01/COLABS
linked-pr: ""
linked-issue: https://github.com/kanya01/COLABS/issues/131
tags: [priority-critical, frontend, dashboard, admin]
updated: 2026-02-24
---

# [FE-02] Admin Dashboard Page

> **Priority**: P0 — Critical | **Phase**: 3 — Frontend | **Effort**: 6–8 hours

## Task
1. Create `src/app/admin/dashboard/page.tsx`
2. Display metrics cards: Users (total, new 7d/30d, verified, banned), Orders (total, active, completed, cancelled, GMV), Revenue (platform fees, pending payouts, total paid), Newsletter (subscribers, confirmed), Errors (unacknowledged)
3. Add trend charts for time-series data (user signups, order volume)
4. Show recent admin activity feed (from audit logs)
5. Show failed Solid Queue jobs panel
6. Professional admin dashboard aesthetic — clean data-dense design

## Acceptance Criteria
- [ ] Dashboard loads all metrics from backend
- [ ] Metrics cards show correct values
- [ ] Trend charts render with appropriate time periods
- [ ] Recent activity feed shows latest admin actions
- [ ] Loading and error states are handled gracefully

## Dependencies
- **Blocked By**: [[open#130] [FE-01] Admin Layout and Auth Guard]], [[open#123] [ADM-07] Admin Dashboard Controller]]
- **Blocks**: None

## Related
- [[Docs/admin/ADMIN_HUB_PLAN]]
- [[open#76] Admin hub]]
