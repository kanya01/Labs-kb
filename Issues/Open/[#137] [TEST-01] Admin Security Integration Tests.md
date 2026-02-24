---
title: "[TEST-01] Admin Security Integration Tests"
type: issue
status: open
linked-repo: kanya01/COLABS
linked-pr: ""
linked-issue: https://github.com/kanya01/COLABS/issues/137
tags: [priority-critical, testing, security, admin]
updated: 2026-02-24
---

# [TEST-01] Admin Security Integration Tests

> **Priority**: P0 — Critical | **Phase**: 4 — Testing | **Effort**: 4–5 hours

## Task
Write integration tests covering:
1. Non-admin cannot access any admin endpoint (all return 403)
2. Unauthenticated user cannot access any admin endpoint (all return 401)
3. `is_admin` cannot be set via user-facing `PATCH /api/v1/users/:id`
4. `is_admin` is not included in user-facing API responses (`GET /api/v1/auth/me`)
5. Banned user receives 403 on all endpoints
6. Banned user cannot login
7. Banned user cannot authenticate via Auth0
8. Unbanning a user restores access

```bash
cd backend && bundle exec rails test test/integration/admin_security_test.rb
```

## Acceptance Criteria
- [ ] All security tests pass
- [ ] Tests cover all auth boundary conditions
- [ ] Test names are descriptive and self-documenting

## Dependencies
- **Blocked By**: [[open#121] [ADM-05] Banned User Enforcement]], [[open#124] [ADM-08] Admin Users Controller]]
- **Blocks**: None

## Related
- [[Docs/testing/TESTING_STRATEGY]]
- [[Docs/admin/ADMIN_HUB_PLAN]]
- [[open#25] Security Audit for Payment and Payout Systems]]
