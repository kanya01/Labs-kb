---
title: Services Workflow Implementation Guide
type: doc
status: complete
linked-repo: https://github.com/kanya01/COLABS
linked-pr: ""
linked-issue: ""
tags: [services, workflow, implementation, guide]
updated: 2026-02-20
---

# Services Workflow Implementation Guide

> Source: [docs/services/SERVICES_WORKFLOW_IMPLEMENTATION_GUIDE.md](https://github.com/kanya01/COLABS/blob/main/docs/services/SERVICES_WORKFLOW_IMPLEMENTATION_GUIDE.md)

Step-by-step implementation reference for the services workflow (tiers, orders, payments, delivery). Used as the primary build guide for Phase 1.

---

## What This Covers

Detailed implementation steps across:
- Backend models and migrations (Service, ServiceTier, Order, OrderRevision)
- Controller logic for order state transitions
- Stripe PaymentIntent and Connect integration hooks
- Active Storage setup for deliverable uploads
- Frontend checkout flow and order management views
- Seller dashboard earnings calculations

---

## Related Notes

- [[Docs/services/SERVICES_WORKFLOW_ENABLEMENT_PLAN]] — Architecture plan this guide implements
- [[Docs/services/SERVICES_WORKFLOW_IMPLEMENTATION_ISSUES]] — GitHub issues tracking the 20 implementation tasks
- [[Docs/services/STRIPE_INTEGRATION]] — Stripe-specific setup
- [[Docs/services/FILE_UPLOAD_GUIDE]] — Active Storage file handling
