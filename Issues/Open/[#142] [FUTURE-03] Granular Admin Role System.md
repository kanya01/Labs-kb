---
title: "[FUTURE-03] Granular Admin Role System"
type: issue
status: open
linked-repo: kanya01/COLABS
linked-pr: ""
linked-issue: https://github.com/kanya01/COLABS/issues/142
tags: [admin, auth, future, roles]
updated: 2026-02-24
---

# [FUTURE-03] Granular Admin Role System

> **Priority**: P3 — Low | **Phase**: Future | **Effort**: 2–3 weeks

## Description
Graduate from `is_admin` boolean to a permission-based system if the team grows. Create an `admin_roles` table with granular permissions (e.g., `can_manage_users`, `can_manage_orders`, `can_view_financials`, `can_manage_newsletter`). Implement a `moderator` role with limited permissions vs. `super_admin` with full access.

## Dependencies
- **Blocked By**: [[open#117] [ADM-01] Database Migrations for Admin Fields]], proven need (>3 admins)
- **Blocks**: None

## Related
- [[Docs/admin/ADMIN_HUB_PLAN]]
- [[open#76] Admin hub]]
