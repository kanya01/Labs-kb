---
title: "[ADM-03] Admin Routes and Base Controller"
type: issue
status: open
linked-repo: kanya01/COLABS
linked-pr: ""
linked-issue: https://github.com/kanya01/COLABS/issues/119
tags: [priority-critical, admin, foundation, routing, controller]
updated: 2026-02-24
---

# [ADM-03] Admin Routes and Base Controller

> **Priority**: P0 — Critical | **Phase**: 1 — Foundation | **Effort**: 1 hour

## Task
1. Create `Api::V1::Admin::BaseController` inheriting from `ApplicationController` and including `AdminAuthorized`
2. Add the `namespace :admin` block to `config/routes.rb` under `api/v1`
3. Include routes for all admin controllers (dashboard, users, orders, newsletter, errors, audit_logs)

## Acceptance Criteria
- [ ] `rails routes | grep admin` shows all expected routes
- [ ] All admin routes resolve to the correct controller actions
- [ ] All admin controllers inherit from `Admin::BaseController`
- [ ] Unauthenticated requests to admin routes → 401
- [ ] Non-admin requests to admin routes → 403

## Dependencies
- **Blocked By**: [[open#118] [ADM-02] Create AdminAuthorized Concern]]
- **Blocks**: #ADM-07, #ADM-08, #ADM-09, #ADM-10, #ADM-11, #ADM-12, #TEST-02

## Related
- [[Docs/admin/ADMIN_HUB_PLAN]]
- [[Docs/api/API_OVERVIEW]]
- [[open#76] Admin hub]]
