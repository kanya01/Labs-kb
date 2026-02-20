---
title: Project Structure — live.o Monorepo
type: doc
status: current
linked-repo: https://github.com/kanya01/COLABS
linked-pr: ""
linked-issue: ""
tags: [design, structure, monorepo]
updated: 2026-02-20
---

# Project Structure — live.o Monorepo

> Source: [docs/design/PROJECT_STRUCTURE.md](https://github.com/kanya01/COLABS/blob/main/docs/design/PROJECT_STRUCTURE.md)

Repository layout for the COLABS monorepo: Next.js frontend at root, Rails API under `/backend`.

---

## Top-Level Layout

```
/                       ← Next.js 15 frontend (TypeScript)
├── app/                ← App Router pages and layouts
├── components/         ← Shared UI components
├── lib/                ← Utilities, API client, hooks
├── public/             ← Static assets
├── backend/            ← Ruby on Rails 8 API
│   ├── app/            ← Models, controllers, services, jobs, mailers
│   ├── config/         ← Routes, database, initializers
│   └── db/             ← Migrations and seeds
├── docs/               ← All documentation (mirrored in this vault)
├── .github/workflows/  ← CI (ci.yml) and deploy (fly-deploy.yml)
├── docker-compose.yml  ← Local dev orchestration
└── .env.example        ← Environment variable template
```

---

## Dev Ports

| Service | Port |
|---|---|
| Frontend (Next.js) | `localhost:3000` |
| Backend (Rails API) | `localhost:4000` |
| Database (PostgreSQL) | `localhost:5432` |

---

## Related Notes

- [[_System Map/Architecture]] — Full system overview
- [[Docs/design/PROJECT_SUMMARY]] — High-level project description
- [[Docs/deployment/DEPLOYMENT_SETUP]] — Docker and Fly.io setup
