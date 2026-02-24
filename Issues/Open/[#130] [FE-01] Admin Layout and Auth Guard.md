---
title: "[FE-01] Admin Layout and Auth Guard"
type: issue
status: open
linked-repo: kanya01/COLABS
linked-pr: ""
linked-issue: https://github.com/kanya01/COLABS/issues/130
tags: [priority-critical, frontend, admin, auth, foundation, layout]
updated: 2026-02-24
---

# [FE-01] Admin Layout and Auth Guard

> **Priority**: P0 — Critical | **Phase**: 3 — Frontend | **Effort**: 4–5 hours

## Task
1. Create `src/app/admin/layout.tsx` — admin layout wrapper with auth guard
2. Check `user.is_admin === true` in layout; redirect non-admins to `/` silently (don't reveal admin exists)
3. Create `AdminSidebar` component with navigation: Dashboard, Users, Orders, Newsletter, Errors, Audit Log
4. Create `AdminHeader` component (admin-specific header, no public navigation)
5. Admin layout should NOT include the public Header/Footer from the root layout
6. Style with a professional, data-dense admin aesthetic (dark sidebar, clean content area)

## Acceptance Criteria
- [ ] Navigating to `/admin/` as a non-admin redirects to `/` with no flash of admin UI
- [ ] Navigating to `/admin/` as an admin shows admin dashboard
- [ ] Sidebar navigation works for all admin pages
- [ ] Admin pages do NOT show the public Header/Footer
- [ ] Loading states are handled (blank screen during auth check)

## Dependencies
- **Blocked By**: [[open#129] [FE-08] Admin API Service and Type Updates]]
- **Blocks**: #FE-02, #FE-03, #FE-04, #FE-05, #FE-06, #FE-07

## Related
- [[Docs/admin/ADMIN_HUB_PLAN]]
- [[open#76] Admin hub]]
