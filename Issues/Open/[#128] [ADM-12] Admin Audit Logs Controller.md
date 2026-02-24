---
title: "[ADM-12] Admin Audit Logs Controller"
type: issue
status: open
linked-repo: kanya01/COLABS
linked-pr: ""
linked-issue: https://github.com/kanya01/COLABS/issues/128
tags: [backend, priority-high, admin, audit]
updated: 2026-02-24
---

# [ADM-12] Admin Audit Logs Controller

> **Priority**: P1 — High | **Phase**: 2 — Backend Controllers | **Effort**: 1–2 hours

## Task
1. Create `Api::V1::Admin::AuditLogsController` inheriting from `Admin::BaseController`
2. `#index` — list all admin actions with filter by admin user, action type, target type, date range, pagination
3. `#show` — full audit log detail including metadata, IP, user agent

## Acceptance Criteria
- [ ] `GET /admin/audit_logs` returns all admin actions sorted by created_at desc
- [ ] `GET /admin/audit_logs?action=user.ban` returns filtered logs
- [ ] `GET /admin/audit_logs?admin_user_id=1` returns logs for specific admin
- [ ] Audit log records are read-only (no update/delete endpoints)

## Dependencies
- **Blocked By**: [[open#119] [ADM-03] Admin Routes and Base Controller]]
- **Blocks**: #FE-07 ([[open#136] [FE-07] Admin Audit Log Page]])

## Related
- [[Docs/admin/ADMIN_HUB_PLAN]]
- [[open#76] Admin hub]]
