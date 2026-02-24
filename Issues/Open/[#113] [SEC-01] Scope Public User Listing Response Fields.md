---
title: "[SEC-01] Scope Public User Listing Response Fields"
type: issue
status: open
linked-repo: kanya01/COLABS
linked-pr: ""
linked-issue: https://github.com/kanya01/COLABS/issues/113
tags: [api, priority-critical, security, pre-admin]
updated: 2026-02-24
---

# [SEC-01] Scope Public User Listing Response Fields

> **Priority**: P0 — Critical | **Phase**: 0 — Security Hardening | **Effort**: 1–2 hours

## Problem
`Api::V1::UsersController#index` has `skip_before_action :authorize_request` and returns `User.all` via `as_json`, which includes `email`, `bio`, `location`, `timezone`, `experience_level`, and other private fields to **unauthenticated requests**.

## Task
1. Create a public-safe user response format returning only: `id`, `name`, `username`, `avatar_url`, `role`, `skills`, `rating`, `portfolio_preview`
2. Apply to unauthenticated `index` and `show` actions
3. Never expose `email`, `location`, `timezone`, `bio`, `experience_level` to unauthenticated callers
4. Update any frontend code that depends on public user listing to use the reduced fields

## Acceptance Criteria
- [ ] `GET /api/v1/users` without auth returns only public fields
- [ ] `GET /api/v1/users/:id` without auth returns only public fields
- [ ] `GET /api/v1/auth/me` (authenticated) still returns full user profile

## Dependencies
- **Blocked By**: None
- **Blocks**: #ADM-01 ([[open#117] [ADM-01] Database Migrations for Admin Fields]])

## Related
- [[Docs/api/API_OVERVIEW]]
- [[open#76] Admin hub]]
