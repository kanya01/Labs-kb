---
title: "[ADM-02] Create AdminAuthorized Concern"
type: issue
status: open
linked-repo: kanya01/COLABS
linked-pr: ""
linked-issue: https://github.com/kanya01/COLABS/issues/118
tags: [priority-critical, admin, auth, concern, foundation]
updated: 2026-02-24
---

# [ADM-02] Create AdminAuthorized Concern

> **Priority**: P0 — Critical | **Phase**: 1 — Foundation | **Effort**: 1 hour

## Task
Create `app/controllers/concerns/admin_authorized.rb` with:
1. `before_action :require_admin!` — checks `current_user.admin?`, returns 403 if false
2. `log_admin_action(action:, target:, metadata:)` helper that creates `AdminAuditLog` entries with IP address and user agent

## Acceptance Criteria
- [ ] Including `AdminAuthorized` in a controller returns 403 for non-admin users
- [ ] Including `AdminAuthorized` in a controller allows access for admin users
- [ ] `log_admin_action` creates an `AdminAuditLog` record with correct fields
- [ ] No token → 401 (from existing `authorize_request`)
- [ ] Regular user token → 403 (from `require_admin!`)
- [ ] Admin user token → 200

## Dependencies
- **Blocked By**: [[open#117] [ADM-01] Database Migrations for Admin Fields]]
- **Blocks**: #ADM-03

## Related
- [[Docs/admin/ADMIN_HUB_PLAN]]
- [[open#76] Admin hub]]
