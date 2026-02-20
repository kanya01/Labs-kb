---
title: Testing Guide — live.o
type: doc
status: current
linked-repo: https://github.com/kanya01/COLABS
linked-pr: ""
linked-issue: ""
tags: [testing, guide, how-to]
updated: 2026-02-20
---

# Testing Guide — live.o

> Source: [docs/testing/TESTING_GUIDE.md](https://github.com/kanya01/COLABS/blob/main/docs/testing/TESTING_GUIDE.md)

How to run and write tests for the live.o platform.

---

## Running Tests

### Frontend

```bash
npm run test          # Jest unit tests
npm run test:e2e      # Cypress E2E tests
npm run lint          # ESLint
npm run type-check    # TypeScript type checking
```

### Backend

```bash
cd backend
bundle exec rspec     # RSpec unit and integration tests
bundle exec rails test # Rails built-in tests (if used)
```

---

## Writing Tests

- **Unit tests** (Jest) — test individual components, hooks, and utility functions in isolation
- **Integration tests** (Jest + React Testing Library) — test component interactions
- **E2E tests** (Cypress) — test full user flows through the browser

Backend:
- **Model specs** — test validations, associations, state machine transitions
- **Request specs** — test API endpoints end-to-end
- **Service specs** — test `NotificationService` and other service objects

---

## CI Integration

Tests run automatically on all pull requests via GitHub Actions (`ci.yml`). See [[Docs/deployment/DEPLOYMENT_SETUP]].

> Note: Lint and type checks are not yet blocking in CI — fixing this is a Phase 3 item. See [[Docs/services/SERVICES_KNOWN_ISSUES]].

---

## Related Notes

- [[Docs/testing/TESTING_STRATEGY]] — Overall testing approach and coverage goals
- [[Docs/testing/FRONTEND_TESTING_PLAN]] — Detailed Cypress and Jest plan
