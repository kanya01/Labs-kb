---
title: Auth0 Setup — live.o OAuth Configuration
type: doc
status: current
linked-repo: https://github.com/kanya01/COLABS
linked-pr: ""
linked-issue: ""
tags: [api, auth, auth0, oauth, security]
updated: 2026-02-20
---

# Auth0 Setup — live.o OAuth Configuration

> Source: [docs/api/AUTH0_SETUP.md](https://github.com/kanya01/COLABS/blob/main/docs/api/AUTH0_SETUP.md)

Guide for configuring Auth0 social login (Google, GitHub) and troubleshooting OAuth flows.

---

## Overview

live.o uses Auth0 for OAuth social login. The Rails backend validates Auth0 JWTs and issues its own 24-hour session tokens.

## Required Environment Variables

```
NEXT_PUBLIC_AUTH0_DOMAIN=your-tenant.auth0.com
NEXT_PUBLIC_AUTH0_CLIENT_ID=your-client-id
AUTH0_CLIENT_SECRET=your-client-secret   # backend only
AUTH0_AUDIENCE=your-api-identifier
```

These must also be set as **GitHub Actions secrets** to enable CI/CD deployment:
- `NEXT_PUBLIC_AUTH0_DOMAIN`
- `NEXT_PUBLIC_AUTH0_CLIENT_ID`

## Social Connections

- **Google** — configured via Auth0 Social Connections
- **GitHub** — configured via Auth0 Social Connections

## Auth Flow

1. User clicks "Sign in with Google/GitHub" on frontend
2. Redirected to Auth0 Universal Login
3. Auth0 handles OAuth, returns `id_token` + `access_token` to callback URL
4. Frontend sends token to Rails API
5. Rails validates token via Auth0 JWKS, issues its own JWT
6. Frontend stores JWT, sends as `Authorization: Bearer <token>` on all requests

---

## Related Notes

- [[Docs/api/API_OVERVIEW]] — Full API reference
- [[_System Map/Architecture]] — Auth component in system overview
- [[Docs/deployment/DEPLOYMENT_SETUP]] — Secrets configuration for Fly.io
