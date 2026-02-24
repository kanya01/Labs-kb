---
title: "[TEST-02] Admin Controller Unit Tests"
type: issue
status: open
linked-repo: kanya01/COLABS
linked-pr: ""
linked-issue: https://github.com/kanya01/COLABS/issues/138
tags: [testing, priority-high, admin, controllers]
updated: 2026-02-24
---

# [TEST-02] Admin Controller Unit Tests

> **Priority**: P1 — High | **Phase**: 4 — Testing | **Effort**: 6–8 hours

## Task
Write controller tests for all admin controllers:
1. `Admin::DashboardController` — returns correct metric structure
2. `Admin::UsersController` — CRUD operations, search/filter, verify/ban/unban with audit logging
3. `Admin::OrdersController` — list, show, force_cancel with service layer integration
4. `Admin::NewsletterController` — list, stats
5. `Admin::ErrorsController` — list, show, acknowledge
6. `Admin::AuditLogsController` — list, show, filter

```bash
cd backend && bundle exec rails test test/controllers/api/v1/admin/
```

## Acceptance Criteria
- [ ] All admin controller actions have corresponding tests
- [ ] Tests verify both success and failure paths
- [ ] Tests verify audit log creation for mutating actions
- [ ] Tests pass with `rails test`

## Dependencies
- **Blocked By**: [[open#119] [ADM-03] Admin Routes and Base Controller]]
- **Blocks**: None

## Related
- [[Docs/testing/TESTING_STRATEGY]]
- [[Docs/admin/ADMIN_HUB_PLAN]]
- [[open#22] End-to-End Integration Tests for Critical Workflows]]
