---
title: Frontend Testing Plan — Cypress & Jest
type: doc
status: in-progress
linked-repo: https://github.com/kanya01/COLABS
linked-pr: ""
linked-issue: ""
tags: [testing, frontend, cypress, jest, e2e]
updated: 2026-02-20
---

# Frontend Testing Plan — Cypress & Jest

> Source: [docs/testing/FRONTEND_TESTING_PLAN.md](https://github.com/kanya01/COLABS/blob/main/docs/testing/FRONTEND_TESTING_PLAN.md)

Detailed plan for Cypress E2E and Jest unit/integration testing on the Next.js frontend.

---

## Jest — Unit & Integration Tests

Key areas targeted:
- **Auth hooks** — token storage, expiry handling, Auth0 callback parsing
- **Service/tier components** — tier selection, pricing display, feature list rendering
- **Order status components** — state badge rendering, revision flow UI
- **API client** — request formation, error handling, retry logic
- **Notification bell** — unread count calculation, mark-read interaction
- **Discovery filters** — filter state management, query string serialisation

## Cypress — E2E Tests

Critical user journeys:
1. **Sign up / login** — email+password and OAuth (Google/GitHub) flows
2. **Discovery** — browse, filter by role, search by keyword
3. **Service purchase** — select tier → checkout → Stripe test payment → order created
4. **Order delivery** — seller uploads deliverable → buyer downloads and approves
5. **Revision flow** — buyer requests revision → seller responds → order completes
6. **Messaging** — send and receive a message between two users
7. **Seller dashboard** — earnings display, payout request flow
8. **Notifications** — receive notification, view notification center

---

## Related Notes

- [[Docs/testing/TESTING_GUIDE]] — How to run these tests
- [[Docs/testing/TESTING_STRATEGY]] — Overall coverage goals and strategy
- [[Docs/deployment/DEPLOYMENT_SETUP]] — CI pipeline that runs tests
