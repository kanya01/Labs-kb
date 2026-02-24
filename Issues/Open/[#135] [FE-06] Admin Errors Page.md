---
title: "[FE-06] Admin Errors Page"
type: issue
status: open
linked-repo: kanya01/COLABS
linked-pr: ""
linked-issue: https://github.com/kanya01/COLABS/issues/135
tags: [frontend, priority-high, admin, observability, errors]
updated: 2026-02-24
---

# [FE-06] Admin Errors Page

> **Priority**: P1 — High | **Phase**: 3 — Frontend | **Effort**: 4–5 hours

## Task
1. Create `src/app/admin/errors/page.tsx` — error log viewer
2. Display: error class, message (truncated), severity badge, timestamp, acknowledged status
3. Filter by severity, acknowledged status, date range
4. Error detail view: full backtrace, request context, user context
5. Acknowledge action button

## Acceptance Criteria
- [ ] Error list loads with most recent first
- [ ] Filters work (severity, acknowledged status)
- [ ] Acknowledging an error updates the UI and records who acknowledged it
- [ ] Backtrace is displayed in a monospace, readable format

## Dependencies
- **Blocked By**: [[open#130] [FE-01] Admin Layout and Auth Guard]], [[open#127] [ADM-11] Admin Errors Controller]]
- **Blocks**: None

## Related
- [[Docs/admin/ADMIN_HUB_PLAN]]
- [[open#76] Admin hub]]
