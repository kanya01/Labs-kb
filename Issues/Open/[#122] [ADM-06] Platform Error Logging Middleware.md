---
title: "[ADM-06] Platform Error Logging Middleware"
type: issue
status: open
linked-repo: kanya01/COLABS
linked-pr: ""
linked-issue: https://github.com/kanya01/COLABS/issues/122
tags: [priority-high, admin, middleware, observability, errors]
updated: 2026-02-24
---

# [ADM-06] Platform Error Logging Middleware

> **Priority**: P1 — High | **Phase**: 1 — Foundation | **Effort**: 2–3 hours

## Task
1. Create `ErrorLogger` class in `app/lib/error_logger.rb`
2. Add `rescue_from StandardError` in `ApplicationController` that logs to `PlatformErrorLog` then re-raises
3. Add error logging to service layer `rescue` blocks (optional, low-priority enrichment)
4. Add scopes to `PlatformErrorLog`: `unacknowledged`, `by_severity`, `recent`

## Acceptance Criteria
- [ ] Controller errors automatically create `PlatformErrorLog` entries
- [ ] Error log includes: class, message, backtrace, request path, user context
- [ ] Self-referential failures (logging itself fails) don't crash the app
- [ ] `PlatformErrorLog.unacknowledged.count` returns correct count

## Dependencies
- **Blocked By**: [[open#117] [ADM-01] Database Migrations for Admin Fields]]
- **Blocks**: #ADM-11 ([[open#127] [ADM-11] Admin Errors Controller]])

## Related
- [[Docs/admin/ADMIN_HUB_PLAN]]
- [[open#76] Admin hub]]
