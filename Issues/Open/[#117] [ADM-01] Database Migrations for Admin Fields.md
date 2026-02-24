---
title: "[ADM-01] Database Migrations for Admin Fields"
type: issue
status: open
linked-repo: kanya01/COLABS
linked-pr: ""
linked-issue: https://github.com/kanya01/COLABS/issues/117
tags: [database, priority-critical, admin, foundation, migration]
updated: 2026-02-24
---

# [ADM-01] Database Migrations for Admin Fields

> **Priority**: P0 — Critical | **Phase**: 1 — Foundation | **Effort**: 1–2 hours

## Task
Create three database migrations:

**Migration 1: Add admin fields to users**
- `is_admin` (boolean, default: false), `verified` (boolean), `banned` (boolean), `banned_at` (datetime), `ban_reason` (string)
- Add indexes on `is_admin`, `banned`, `verified`

**Migration 2**: Create `admin_audit_logs` table

**Migration 3**: Create `platform_error_logs` table

Also:
- Update `User` model with `admin?`, `banned?` methods
- Ensure `is_admin` is excluded from `as_json` output and `user_params`
- Create `AdminAuditLog` model
- Create `PlatformErrorLog` model
- Seed first admin user via Rake task

## Acceptance Criteria
- [ ] Migrations run without errors (`rails db:migrate`)
- [ ] `User.first.admin?` returns false
- [ ] `User.first.update!(is_admin: true)` → `User.first.admin?` returns true
- [ ] `AdminAuditLog.create!(...)` works with required fields
- [ ] `PlatformErrorLog.create!(...)` works with required fields
- [ ] `as_json` for User does NOT include `is_admin`, `banned`, `verified` fields in user-facing responses
- [ ] Rake task to promote first admin exists and works

## Dependencies
- **Blocked By**: [[open#113] [SEC-01] Scope Public User Listing Response Fields]], [[open#114] [SEC-02] Protect Admin Fields from User Params]]
- **Blocks**: #ADM-02, #ADM-03, #ADM-04, #ADM-05, #ADM-06, #TEST-03

## Related
- [[Docs/admin/ADMIN_HUB_PLAN]]
- [[open#76] Admin hub]]
