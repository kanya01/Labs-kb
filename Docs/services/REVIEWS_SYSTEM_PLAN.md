---
title: Reviews System Plan
type: doc
status: planned
linked-repo: https://github.com/kanya01/COLABS
linked-pr: ""
linked-issue: ""
tags: [services, reviews, ratings, planned]
updated: 2026-02-20
---

# Reviews System Plan

> Source: [docs/services/REVIEWS_SYSTEM_PLAN.md](https://github.com/kanya01/COLABS/blob/main/docs/services/REVIEWS_SYSTEM_PLAN.md)

Plan to replace hardcoded `rating` / `reviewsCount` values with a real review model. Phase 6a of [[Docs/PLATFORM_ROADMAP]].

---

## Goals

- **Review model** — tied to completed orders (1 review per order, buyer → seller)
- **Star ratings** — 1–5 scale, aggregate computed and stored on Service
- **Seller responses** — sellers can reply to reviews
- **Review display** — shown on profiles, service pages, and gig cards
- **Replace hardcoded values** — live `rating` and `reviews_count` fields pulled from DB

**Estimated effort**: 2–3 weeks

---

## Data Model

```
Review
  - order_id (unique — one review per order)
  - reviewer_id (buyer)
  - reviewee_id (seller)
  - service_id
  - rating: integer (1–5)
  - body: text
  - seller_response: text (optional)
  - created_at
```

---

## Related Notes

- [[Docs/services/SERVICES_WORKFLOW_ENABLEMENT_PLAN]] — Order model context
- [[Docs/design/SYSTEM_ONTOLOGY]] — Domain model
- [[Docs/PLATFORM_ROADMAP]] — Phase 6a
