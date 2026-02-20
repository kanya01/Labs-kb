---
title: Services Known Issues — Tech Debt Tracker
type: doc
status: in-progress
linked-repo: https://github.com/kanya01/COLABS
linked-pr: ""
linked-issue: ""
tags: [services, tech-debt, known-issues]
updated: 2026-02-20
---

# Services Known Issues — Tech Debt Tracker

> Source: [docs/services/SERVICES_KNOWN_ISSUES.md](https://github.com/kanya01/COLABS/blob/main/docs/services/SERVICES_KNOWN_ISSUES.md)

Four tech debt items to resolve before adding new features (Phase 3 of [[Docs/PLATFORM_ROADMAP]]).

---

## Issue 1 — Hardcoded Service Data

**Priority**: P1 | **Effort**: 2–3 days

Some frontend components reference static arrays for service listings, categories, and featured content instead of fetching from the API. Must be replaced with dynamic fetching before data can evolve.

## Issue 2 — Orders and Sells Scoped to Every User

**Priority**: P1 | **Effort**: 2–3 days

Orders are not fully scoped by user role — buyers may see seller data and vice versa. Self-purchase prevention not fully enforced. Dashboard metrics may not be user-scoped.

## Issue 3 — Auth Persistence Investigation Needed

**Priority**: P2 | **Effort**: 3–5 days (investigation + implementation)

Auth state does not persist reliably across browser restarts, tabs, or token expiry. Needs investigation covering: token refresh, cross-tab synchronization, and session recovery.

## Issue 4 — Failing Lint and Type Checks

**Priority**: P1 | **Effort**: 2–3 days

Accumulated ESLint violations and TypeScript type check failures. Lint and type checks are not currently blocking in CI — must be made blocking once fixed.

---

## Related Notes

- [[Docs/PLATFORM_ROADMAP]] — Phase 3 context
- [[Docs/services/SERVICES_WORKFLOW_ENABLEMENT_PLAN]] — Original implementation plan
