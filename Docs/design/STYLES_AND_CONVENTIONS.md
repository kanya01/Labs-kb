---
title: Styles & Conventions — live.o
type: doc
status: current
linked-repo: https://github.com/kanya01/COLABS
linked-pr: ""
linked-issue: ""
tags: [design, css, conventions, tokens]
updated: 2026-02-20
---

# Styles & Conventions — live.o

> Source: [docs/design/STYLES_AND_CONVENTIONS.md](https://github.com/kanya01/COLABS/blob/main/docs/design/STYLES_AND_CONVENTIONS.md)

CSS conventions and design token reference for the live.o frontend.

---

## Stack

- **Tailwind CSS** — utility-first, configured with custom tokens
- **TypeScript** — all frontend code is typed
- **ESLint + Prettier** — enforced code style

---

## Key Conventions

- Dark theme as baseline (no light mode toggle currently)
- Component files use PascalCase: `ServiceCard.tsx`, `OrderStatus.tsx`
- Shared UI primitives live in `/components/ui/`
- Page-level components in `/app/(route)/page.tsx` following Next.js App Router conventions
- API calls go through a centralised client in `/lib/api/`

---

## Related Notes

- [[Docs/design/DESIGN_AND_ROADMAP]] — Visual design principles
- [[Docs/design/PROJECT_STRUCTURE]] — Where files live
