---
title: Deployment Setup — Fly.io, Docker, CI/CD
type: doc
status: current
linked-repo: https://github.com/kanya01/COLABS
linked-pr: ""
linked-issue: ""
tags: [deployment, fly-io, docker, ci-cd, github-actions]
updated: 2026-02-20
---

# Deployment Setup — Fly.io, Docker, CI/CD

> Source: [docs/deployment/DEPLOYMENT_SETUP.md](https://github.com/kanya01/COLABS/blob/main/docs/deployment/DEPLOYMENT_SETUP.md)

Complete deployment reference for the live.o platform on Fly.io.

---

## Local Dev (Docker Compose)

```bash
cp .env.example .env.local
docker-compose up --build
```

Starts frontend (`:3000`), backend (`:4000`), and PostgreSQL (`:5432`).

---

## CI/CD Pipeline (GitHub Actions)

Two workflows:

| Workflow | Trigger | What it does |
|---|---|---|
| `ci.yml` | Pull requests | Lint, type check, build (frontend); Rails tests (backend) |
| `fly-deploy.yml` | Push to `main` | Auto-deploys to Fly.io |

### Required GitHub Secrets

| Secret | Source |
|---|---|
| `FLY_API_TOKEN` | `flyctl auth token` |
| `NEXT_PUBLIC_AUTH0_DOMAIN` | Auth0 dashboard |
| `NEXT_PUBLIC_AUTH0_CLIENT_ID` | Auth0 dashboard |

---

## Fly.io Deployment

- Both frontend and backend are containerised and deployed as separate Fly apps
- Database (PostgreSQL) provisioned via Fly Postgres
- Environment variables set via `flyctl secrets set`

---

## Related Notes

- [[Docs/api/AUTH0_SETUP]] — Auth0 secrets configuration
- [[_System Map/Architecture]] — Infrastructure overview
