---
title: "[SEC-02] Protect Admin Fields from User Params"
type: issue
status: open
linked-repo: kanya01/COLABS
linked-pr: ""
linked-issue: https://github.com/kanya01/COLABS/issues/114
tags: [api, priority-critical, security, pre-admin]
updated: 2026-02-24
---

# [SEC-02] Protect Admin Fields from User Params

> **Priority**: P0 — Critical | **Phase**: 0 — Security Hardening | **Effort**: 1 hour

## Problem
`user_params` permits `:role` and other fields for both `create` and `update`. When `is_admin`, `verified`, and `banned` columns are added, there is risk of privilege escalation if these are accidentally included in the permit list.

> **IMPORTANT**: The `role` field should **remain permitted and unvalidated** — it's a freeform creative identity.

## Task
1. Add an explicit comment block above `user_params` documenting which fields are intentionally excluded (`is_admin`, `verified`, `banned`, `banned_at`, `ban_reason`)
2. Ensure these fields are never included in any user-facing `params.permit(...)` call
3. Write integration tests verifying `PATCH /api/v1/users/:id` with `is_admin: true` does NOT change the field
4. Write integration tests verifying `PATCH /api/v1/users/:id` with `banned: true` does NOT change the field

## Acceptance Criteria
- [ ] `PATCH /api/v1/users/:id` with `is_admin: true` → field remains `false`
- [ ] `PATCH /api/v1/users/:id` with `banned: true` → field remains `false`
- [ ] `PATCH /api/v1/users/:id` with `verified: true` → field remains `false`
- [ ] `PATCH /api/v1/users/:id` with `role: "Beat Maker"` → field updates normally
- [ ] Comment block above `user_params` explains the exclusion

## Dependencies
- **Blocked By**: None
- **Blocks**: #ADM-01 ([[open#117] [ADM-01] Database Migrations for Admin Fields]])

## Related
- [[Docs/api/API_OVERVIEW]]
- [[open#76] Admin hub]]
