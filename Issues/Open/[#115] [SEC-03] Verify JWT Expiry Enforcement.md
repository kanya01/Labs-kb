---
title: "[SEC-03] Verify JWT Expiry Enforcement"
type: issue
status: open
linked-repo: kanya01/COLABS
linked-pr: ""
linked-issue: https://github.com/kanya01/COLABS/issues/115
tags: [security, auth, investigation]
updated: 2026-02-24
---

# [SEC-03] Verify JWT Expiry Enforcement

> **Priority**: P1 — High | **Phase**: 0 — Security Hardening | **Effort**: 1–2 hours

## Problem
`ApplicationController#authorize_request` decodes JWT via `JsonWebToken.decode(header)`. It's unclear whether the decode method enforces `exp` (expiry), `iss` (issuer), or `aud` (audience) claims. If expiry is not enforced, tokens never expire and stolen tokens grant permanent access.

## Task
1. Locate and review `JsonWebToken` implementation (likely in `app/lib/` or `lib/`)
2. Verify that `exp` claim is set during `encode` and verified during `decode`
3. If missing, add expiry enforcement (24 hours)
4. Consider adding `iss` (issuer) claim for defense in depth
5. Document findings

## Acceptance Criteria
- [ ] Expired JWT tokens return 401
- [ ] Token format includes `exp` claim
- [ ] Documentation updated with auth flow details

## Dependencies
- **Blocked By**: None
- **Blocks**: None (non-blocking but important)

## Related
- [[Docs/api/AUTH0_SETUP]]
- [[Docs/api/API_OVERVIEW]]
