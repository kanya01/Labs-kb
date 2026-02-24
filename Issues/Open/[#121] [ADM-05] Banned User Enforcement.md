---
title: "[ADM-05] Banned User Enforcement"
type: issue
status: open
linked-repo: kanya01/COLABS
linked-pr: ""
linked-issue: https://github.com/kanya01/COLABS/issues/121
tags: [priority-critical, security, admin, auth, foundation]
updated: 2026-02-24
---

# [ADM-05] Banned User Enforcement

> **Priority**: P0 — Critical | **Phase**: 1 — Foundation | **Effort**: 2–3 hours

## Task
1. Add `check_banned!` `before_action` to `ApplicationController` (runs after `authorize_request`)
2. Banned users receive a 403 with `{ error: "Account suspended", reason: "..." }` on all API calls
3. Reject banned users at login (`AuthenticationController#login`)
4. Reject banned users at Auth0 callback (`Auth0Controller#callback`)
5. Frontend `api.ts` interceptor should handle 403 "Account suspended" differently from generic 403

## Acceptance Criteria
- [ ] Banned user's JWT bearer request → 403 with ban reason
- [ ] Banned user's login attempt → 401 or 403 with message "Account suspended"
- [ ] Banned user's Auth0 callback → 403
- [ ] Unbanning user → all endpoints accessible again
- [ ] Non-banned users unaffected

## Dependencies
- **Blocked By**: [[open#117] [ADM-01] Database Migrations for Admin Fields]]
- **Blocks**: #TEST-01 ([[open#137] [TEST-01] Admin Security Integration Tests]])

## Related
- [[Docs/admin/ADMIN_HUB_PLAN]]
- [[Docs/api/AUTH0_SETUP]]
- [[open#25] Security Audit for Payment and Payout Systems]]
