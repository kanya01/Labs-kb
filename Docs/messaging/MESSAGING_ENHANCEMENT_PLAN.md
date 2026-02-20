---
title: Messaging Enhancement Plan — Service-Oriented Messaging v2
type: doc
status: planned
linked-repo: https://github.com/kanya01/COLABS
linked-pr: ""
linked-issue: ""
tags: [messaging, planned, collaboration]
updated: 2026-02-20
---

# Messaging Enhancement Plan — Service-Oriented Messaging v2

> Source: [docs/messaging/MESSAGING_ENHANCEMENT_PLAN.md](https://github.com/kanya01/COLABS/blob/main/docs/messaging/MESSAGING_ENHANCEMENT_PLAN.md)

Plan to transform basic text messaging into a full service collaboration hub. Phase 6b of [[Docs/PLATFORM_ROADMAP]]. Estimated effort: 4–6 weeks.

---

## Current State

Direct user-to-user text conversations with read status tracking. No file sharing, no service context.

## Planned Capabilities

- **File sharing** — Share audio, images, and documents directly in chat
- **Service offers** — Send a service proposal (tier, price, terms) as a structured message card
- **Order initiation** — Accept an offer → create order → payment flow, all from within the chat thread
- **Order updates in thread** — Status changes and deliverables surfaced as message badges in the conversation
- **Rich message types** — File cards, offer cards, order update badges
- **Read receipts** — Per-message read indicators

## New Message Types

```
text        — existing plain text
file        — uploaded file attachment
offer       — service offer with tier/price/terms
order_event — status update badge (paid, delivered, etc.)
```

---

## Related Notes

- [[Docs/services/SERVICES_WORKFLOW_ENABLEMENT_PLAN]] — Order model that messaging will connect to
- [[Docs/services/FILE_UPLOAD_GUIDE]] — File infrastructure to leverage
- [[Docs/PLATFORM_ROADMAP]] — Phase 6b
- [[_System Map/Architecture]] — Current messaging component
