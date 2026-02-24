---
title: "[ADM-11] Admin Errors Controller"
type: issue
status: open
linked-repo: kanya01/COLABS
linked-pr: ""
linked-issue: https://github.com/kanya01/COLABS/issues/127
tags: [backend, priority-high, admin, observability, errors]
updated: 2026-02-24
---

# [ADM-11] Admin Errors Controller

> **Priority**: P1 — High | **Phase**: 2 — Backend Controllers | **Effort**: 2–3 hours

## Task
1. Create `Api::V1::Admin::ErrorsController` inheriting from `Admin::BaseController`
2. `#index` — list errors with filter by severity, acknowledged status, date range, pagination
3. `#show` — full error detail including backtrace, request context, user context
4. `#acknowledge` — mark error as acknowledged, record who acknowledged it, log admin action

## Acceptance Criteria
- [ ] `GET /admin/errors` returns platform errors sorted by created_at desc
- [ ] `GET /admin/errors?severity=critical&acknowledged=false` returns filtered errors
- [ ] `PATCH /admin/errors/:id/acknowledge` marks error as acknowledged
- [ ] Acknowledged errors show `acknowledged_by_id` and `acknowledged_at`

## Dependencies
- **Blocked By**: [[open#119] [ADM-03] Admin Routes and Base Controller]], [[open#122] [ADM-06] Platform Error Logging Middleware]]
- **Blocks**: #FE-06 ([[open#135] [FE-06] Admin Errors Page]])

## Related
- [[Docs/admin/ADMIN_HUB_PLAN]]
- [[open#76] Admin hub]]
