---
title: "[FE-05] Admin Newsletter Page"
type: issue
status: open
linked-repo: kanya01/COLABS
linked-pr: ""
linked-issue: https://github.com/kanya01/COLABS/issues/134
tags: [frontend, admin, newsletter]
updated: 2026-02-24
---

# [FE-05] Admin Newsletter Page

> **Priority**: P2 — Medium | **Phase**: 3 — Frontend | **Effort**: 3–4 hours

## Task
1. Create `src/app/admin/newsletter/page.tsx` — subscriber list and stats
2. Display subscriber list with: email, status, confirmed_at, source
3. Stats panel: total, confirmed, unsubscribed, recent trend

## Acceptance Criteria
- [ ] Subscriber list loads and displays correctly
- [ ] Stats panel shows accurate counts
- [ ] Status badges (active, unsubscribed, pending) are color-coded

## Dependencies
- **Blocked By**: [[open#130] [FE-01] Admin Layout and Auth Guard]], [[open#126] [ADM-10] Admin Newsletter Controller]]
- **Blocks**: None

## Related
- [[Docs/admin/ADMIN_HUB_PLAN]]
- [[Docs/email/EMAIL_NOTIFICATION_STATUS]]
- [[open#76] Admin hub]]
