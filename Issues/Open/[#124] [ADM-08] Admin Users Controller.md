---
title: "[ADM-08] Admin Users Controller"
type: issue
status: open
linked-repo: kanya01/COLABS
linked-pr: ""
linked-issue: https://github.com/kanya01/COLABS/issues/124
tags: [backend, priority-critical, admin, users]
updated: 2026-02-24
---

# [ADM-08] Admin Users Controller

> **Priority**: P0 — Critical | **Phase**: 2 — Backend Controllers | **Effort**: 4–5 hours

## Task
1. Create `Api::V1::Admin::UsersController` inheriting from `Admin::BaseController`
2. `#index` — list all users with search (name, email, username), filter (role, banned, verified), pagination
3. `#show` — full user detail including order count (as buyer/seller), earnings, services count
4. `#verify` / `#unverify` — set `verified` flag, log admin action
5. `#ban` — set `banned: true, banned_at, ban_reason`, log admin action, send notification
6. `#unban` — clear ban fields, log admin action, send notification
7. All mutating actions create `AdminAuditLog` entries via `log_admin_action`

## Acceptance Criteria
- [ ] `GET /admin/users?search=john` returns matching users
- [ ] `GET /admin/users?filter=banned` returns only banned users
- [ ] `PATCH /admin/users/:id/verify` sets verified=true and creates audit log
- [ ] `PATCH /admin/users/:id/ban` sets banned=true, logs, and sends notification to user
- [ ] `PATCH /admin/users/:id/unban` clears ban, logs, and sends notification to user
- [ ] Non-admin requests return 403

## Dependencies
- **Blocked By**: [[open#119] [ADM-03] Admin Routes and Base Controller]], [[open#120] [ADM-04] Audit Log Model and Service]]
- **Blocks**: #FE-03 ([[open#132] [FE-03] Admin User Management Page]]), #TEST-01

## Related
- [[Docs/admin/ADMIN_HUB_PLAN]]
- [[open#76] Admin hub]]
