---
title: Email System Plan
type: doc
status: complete
linked-repo: https://github.com/kanya01/COLABS
linked-pr: ""
linked-issue: ""
tags: [email, notifications, architecture, planning]
updated: 2026-02-20
---

# Email System Plan

> Source: [docs/email/EMAIL_SYSTEM_PLAN.md](https://github.com/kanya01/COLABS/blob/main/docs/email/EMAIL_SYSTEM_PLAN.md)

Original architecture plan for the email and notification system (Phase 2). All 12 issues have been implemented. See [[Docs/email/EMAIL_NOTIFICATION_STATUS]] for current state.

---

## Architecture

- **Resend** for email delivery — chosen over SMTP for reliability and template management
- **NotificationService** — single entry point that fans out to in-app notification record + email job
- **SolidQueue** — Rails async job queue; `SendNotificationEmailJob` handles delivery
- **In-app notifications** — stored in `notifications` table, 12 event types, polled by frontend

## Email Categories

1. **Transactional** — order lifecycle events (created, paid, in_progress, in_review, completed)
2. **Activity** — messages, revision requests/responses
3. **Financial** — earnings available, payout completed
4. **Marketing** — newsletter broadcasts (double opt-in subscriber system)
5. **Welcome** — onboarding email on registration

## Newsletter System

- Subscribers sign up via site footer
- Double opt-in: confirmation email → click to confirm
- Managed via `subscribers` table
- Broadcast from admin panel (Phase 4 — [[Docs/admin/ADMIN_HUB_PLAN]])

---

## Related Notes

- [[Docs/email/EMAIL_NOTIFICATION_STATUS]] — Implemented state
- [[Docs/email/EMAIL_SYSTEM_ISSUES]] — GitHub issue specifications
- [[_System Map/Architecture]] — Email in the full system
