---
title: Testing Strategy — live.o
type: doc
status: current
linked-repo: https://github.com/kanya01/COLABS
linked-pr: ""
linked-issue: ""
tags: [testing, strategy, coverage]
updated: 2026-02-20
---

# Testing Strategy — live.o

> Source: [docs/testing/TESTING_STRATEGY.md](https://github.com/kanya01/COLABS/blob/main/docs/testing/TESTING_STRATEGY.md)

Overall testing approach and coverage goals for the live.o platform.

---

## Testing Pyramid

```
        [E2E — Cypress]           ← critical user journeys
      [Integration — RTL]         ← component interactions
    [Unit — Jest / RSpec]         ← logic, models, utilities
```

## Coverage Goals

- **Target**: 90%+ coverage (Phase 7 goal per [[Docs/PLATFORM_ROADMAP]])
- **Current state**: partial — backend has some model and request specs; frontend testing is in progress per [[Docs/testing/FRONTEND_TESTING_PLAN]]

## Priority Test Areas

1. Order lifecycle state machine (critical business logic)
2. Stripe payment and webhook flows
3. Auth flows (JWT issuance, Auth0 callback)
4. Service tier creation and validation
5. Notification dispatch (NotificationService)
6. Discovery page filtering and search

---

## Related Notes

- [[Docs/testing/TESTING_GUIDE]] — How to run tests
- [[Docs/testing/FRONTEND_TESTING_PLAN]] — Cypress E2E and Jest plan
