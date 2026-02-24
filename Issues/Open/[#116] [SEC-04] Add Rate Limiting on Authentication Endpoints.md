---
title: "[SEC-04] Add Rate Limiting on Authentication Endpoints"
type: issue
status: open
linked-repo: kanya01/COLABS
linked-pr: ""
linked-issue: https://github.com/kanya01/COLABS/issues/116
tags: [security, infrastructure, priority-high, pre-admin, auth]
updated: 2026-02-24
---

# [SEC-04] Add Rate Limiting on Authentication Endpoints

> **Priority**: P1 — High | **Phase**: 0 — Security Hardening | **Effort**: 2–3 hours

## Problem
No rate limiting exists on `/api/v1/auth/login` or `/api/v1/auth/auth0`. Brute-force and credential-stuffing attacks are trivially possible.

## Task
1. Add `rack-attack` gem to Gemfile
2. Configure rate limits:
   - Login: 5 requests per minute per IP
   - Signup: 3 requests per minute per IP
   - Auth0 callback: 10 requests per minute per IP
   - General API: 100 requests per minute per IP
3. Return 429 status with `Retry-After` header when rate limited
4. Add tests for rate limiting behavior

## Acceptance Criteria
- [ ] 6th login attempt within 1 minute from same IP returns 429
- [ ] Normal usage is unaffected
- [ ] Rate limit response includes `Retry-After` header

## Dependencies
- **Blocked By**: None
- **Blocks**: #ADM-01 (soft block — recommended before admin)

## Related
- [[Docs/api/AUTH0_SETUP]]
- [[Docs/api/API_OVERVIEW]]
- [[open#76] Admin hub]]
