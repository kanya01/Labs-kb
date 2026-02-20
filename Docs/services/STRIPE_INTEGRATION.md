---
title: Stripe Integration — Payments & Connect
type: doc
status: current
linked-repo: https://github.com/kanya01/COLABS
linked-pr: ""
linked-issue: ""
tags: [services, payments, stripe, connect]
updated: 2026-02-20
---

# Stripe Integration — Payments & Connect

> Source: [docs/services/STRIPE_INTEGRATION.md](https://github.com/kanya01/COLABS/blob/main/docs/services/STRIPE_INTEGRATION.md)

Stripe payment and Connect payout setup for live.o.

---

## Payment Flow (Buyers)

1. Buyer selects a service tier and proceeds to checkout
2. Backend creates a `PaymentIntent` via Stripe API
3. Frontend renders **Stripe Elements** for card input
4. On confirmation, Stripe processes payment and fires webhook
5. `payment_intent.succeeded` webhook → order transitions to `paid` → `in_progress`

## Payout Flow (Sellers)

1. Sellers onboard via **Stripe Connect** (Express account)
2. Earnings held for **14 days** before becoming available
3. Seller requests payout from dashboard
4. Backend creates a `Transfer` to the seller's Connect account

## Webhooks Handled

| Event | Action |
|---|---|
| `payment_intent.succeeded` | Order → paid, notify buyer + seller |
| `payment_intent.payment_failed` | Order → failed, notify buyer |
| `payment_intent.canceled` | Order → canceled |

## Environment Variables Required

```
STRIPE_SECRET_KEY
STRIPE_WEBHOOK_SECRET
STRIPE_CONNECT_CLIENT_ID
NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY
```

---

## Related Notes

- [[Docs/services/SERVICES_WORKFLOW_ENABLEMENT_PLAN]] — Full order workflow
- [[Docs/api/API_OVERVIEW]] — Stripe API endpoints
- [[_System Map/Architecture]] — Payment layer in system overview
