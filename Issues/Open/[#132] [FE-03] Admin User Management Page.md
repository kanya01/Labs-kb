---
title: "[FE-03] Admin User Management Page"
type: issue
status: open
linked-repo: kanya01/COLABS
linked-pr: ""
linked-issue: https://github.com/kanya01/COLABS/issues/132
tags: [priority-critical, frontend, admin, users]
updated: 2026-02-24
---

# [FE-03] Admin User Management Page

> **Priority**: P0 — Critical | **Phase**: 3 — Frontend | **Effort**: 8–10 hours

## Task
1. Create `src/app/admin/users/page.tsx` — user list with search, filter (role, banned, verified), sort, pagination
2. Create `src/app/admin/users/[id]/page.tsx` — user detail page with profile, orders summary, earnings, services
3. Add action buttons: Verify, Unverify, Ban (with reason dialog), Unban
4. Show confirmation dialogs before destructive actions
5. Show admin audit trail for this specific user on the detail page
6. Create reusable `DataTable` component for sortable/filterable tables

## Acceptance Criteria
- [ ] User list supports real-time search (debounced)
- [ ] Filters work correctly (role, banned, verified)
- [ ] User detail page shows comprehensive user data
- [ ] Ban action requires reason input
- [ ] All actions use confirmation dialogs
- [ ] Actions update UI optimistically
- [ ] Audit trail is visible on user detail page

## Dependencies
- **Blocked By**: [[open#130] [FE-01] Admin Layout and Auth Guard]], [[open#124] [ADM-08] Admin Users Controller]]
- **Blocks**: None

## Related
- [[Docs/admin/ADMIN_HUB_PLAN]]
- [[open#76] Admin hub]]
