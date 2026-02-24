---
title: "[FE-08] Admin API Service and Type Updates"
type: issue
status: open
linked-repo: kanya01/COLABS
linked-pr: ""
linked-issue: https://github.com/kanya01/COLABS/issues/129
tags: [api, priority-critical, frontend, admin, foundation, types]
updated: 2026-02-24
---

# [FE-08] Admin API Service and Type Updates

> **Priority**: P0 — Critical | **Phase**: 3 — Frontend | **Effort**: 1–2 hours

## Task
1. Update `src/types/index.ts` — add `is_admin?`, `verified?`, `banned?`, `banned_at?`, `ban_reason?` to `User` interface
2. Create `src/lib/admin-service.ts` — centralized admin API client with all admin endpoints
3. Ensure the auth store (`src/lib/store.ts`) returns admin status correctly

## Acceptance Criteria
- [ ] `User` type includes all new optional admin fields
- [ ] `AdminService.getDashboard()` calls `GET /api/v1/admin/dashboard`
- [ ] All admin API calls use the existing `api` client with JWT auth
- [ ] TypeScript compilation passes (`npx tsc --noEmit`)

## Dependencies
- **Blocked By**: [[open#117] [ADM-01] Database Migrations for Admin Fields]]
- **Blocks**: #FE-01 ([[open#130] [FE-01] Admin Layout and Auth Guard]])

## Related
- [[Docs/admin/ADMIN_HUB_PLAN]]
- [[Docs/api/API_OVERVIEW]]
- [[open#54] Fix failing lint & type checks]]
- [[open#76] Admin hub]]
