---
type: "[[Task]]"
categories:
  - "[[Work]]"
  - "[[Tasks]]"
organization:
  - "[[aiquery.io]]"
projects:
  - "[[aq-client]]"
status:
  - active
priority: P2
date: 2026-05-05
tags:
  - team-settings
  - role-management
  - invitations
related-meetings:
  - "[[260505T1905 (Tue) Weekly Scrum Meeting]]"
---

## Overview

Team Settings enhancements covering the invitation flow, role assignment, user type visibility, and access restrictions for Liveshell. Derived from the [[260505T1905 (Tue) Weekly Scrum Meeting|2026-05-05 Weekly Scrum]].

## Role Permissions Reference

| Action | ROOT | ADMIN | POWER USER | USER |
|---|:---:|:---:|:---:|:---:|
| Send invites | ✓ | ✓ | | |
| Change user role | ✓ | ✓ | | |
| Transfer ownership | ✓ | | | |
| Liveshell access | ✓ | ✓ | ✓ | |
| Create API roles | ✓ | ✓ | ✓ | |

> A user's role cannot be changed to `ROOT`. Root users' roles cannot be changed by Admins.

## Tasks

### Create Invitation Dialog

- [ ] Add role selector to the Create Invitation dialog — each role option needs a label + short description.
- [ ] Ensure user type (role) is shown as a visible/required column in the invitations table.

### Role Change Restrictions

- [ ] Enforce that **Change User Role** is a ROOT-only action.
- [ ] Restrict target roles to `POWER USER` or `USER` — changing any user to `ROOT` must be blocked.

### Access Control

- [ ] Restrict Liveshell access to `POWER USER`, `ADMIN`, and `ROOT` only.

### Power User Invite Flow

- [ ] Clarify scope of "develop the power user invite flow" with Rajput — scope TBD.
