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
related-meetings:
  - "[[260505 Weekly Scrum Meeting]]"
---

## Overview

Team Settings enhancements covering the invitation flow, role assignment, user type visibility, and access restrictions for Liveshell. Derived from the [[260505 Weekly Scrum Meeting|2026-05-05 Weekly Scrum]].

## Role Permissions Reference

| Action             | ROOT | ADMIN | POWER USER | USER |
| ------------------ | :--: | :---: | :--------: | :--: |
| Send invites       |  ✓   |   ✓   |            |      |
| Change user role   |  ✓   |   ✓   |            |      |
| Transfer ownership |  ✓   |       |            |      |
| Liveshell access   |  ✓   |   ✓   |     ✓      |      |
| Create API roles   |  ✓   |   ✓   |     ✓      |      |

> A user's role cannot be changed to `ROOT`. Root users' roles cannot be changed by Admins.

## Tasks

### Create Invitation Dialog

- [x] Add role selector to the Create Invitation dialog — each role option needs a label + short description.
- [x] Ensure user type (role) is shown as a visible/required column in the invitations table.

### Role Change Restrictions

- [x] Enforce that **Change User Role** is a ROOT-only action.
- [x] Restrict target roles to `POWER USER` or `USER` — changing any user to `ROOT` must be blocked.

### Access Control

- [x] Restrict Liveshell access to `POWER USER`, `ADMIN`, and `ROOT` only.

### Power User Invite Flow

- [x] Clarify scope of "develop the power user invite flow" with Rajput — scope TBD.

## Optimization
- [ ] Create a Centralized Roles and Permission Class/Hooks, which allows receiving membership/role etc and based on that return callbacks to evaluate the access to different areas of the applications.
- [ ] Refactor and optimize the code of the features PR
	- [ ] use the `toast.promise` pattern in `src/application/hooks/membership.hook.ts`
	- [ ] refactor the utils in a centralized class
	- [ ] simplify/refactor the `src/client/views/settings/invite-settings/invite-setting-create-dialog.tsx`
	- [ ] Allow modifying the select-input's option-item to custom items
	- [ ] Instead of a dedicated check for `user` role in `src/client/views/settings/invite-settings/invite-table-columns.tsx`, a non-conditional uppercase function would have been better
