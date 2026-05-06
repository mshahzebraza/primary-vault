---
type: "[[Meeting]]"
categories:
  - "[[Meetings]]"
  - "[[Work]]"
date: 2026-05-05
tags:
  - scrum
  - weekly
organization:
  - "[[aiquery.io]]"
projects:
  - "[[aq-client]]"
attendees:
  - "[[Rajput]]"
status:
  - active
---

## Context

Weekly scrum covering UI/UX improvements across Settings, Team Management, and the Rapid Response view. Also aligned on role-permission rules for team actions.

---

## Discussion

### Settings

- [x] Split the settings views (Account and Security tabs — confirmed in dev meeting).
- Update the feature tracking sheet to reflect newly shipped features.

### Auth UX

- **Issue:** A logged-in user can navigate to `/auth/login` via the URL bar and see the login page.
- **Options:**
  - Document it as a known minor UX issue and leave it.
  - Guard the route so it redirects authenticated users away from `/auth/login`.
- **Unconfirmed:** When the screen is on sleep, the inactivity timeout may not log the user out — needs verification.

### Team Settings & Role Management

- Add role selection to the **Create Invitation** dialog; each role option must include a label and a short description.
- User type must be visible/required in the invitations table.
- **Change User Role** action is restricted to the `ROOT` user.
  - A user's role can only be changed to `POWER USER` or `USER` — not to `ROOT`.
- **Liveshell** access is restricted to `POWER USER`, `ADMIN`, and `ROOT`.
- Power user invite flow needs to be developed — scope TBD (needs clarification from Rajput).

### Rapid Response View

- The primary sidebar should auto-close when Query Smith opens.
- Remove the **Load Query** button in favour of click-to-load behaviour.
- Add an **Actions** dropdown button with the following options:
  - Load from preset
  - Save as preset *(also expose this action on individual query history items)*
  - Go to Create Query
- *(Optional)* Multi-select on query history items to batch-save as a query preset.

---

## Role Permissions Reference

| Action | ROOT | ADMIN | POWER USER | USER |
|---|:---:|:---:|:---:|:---:|
| Send invites | ✓ | ✓ | | |
| Change user role | ✓ | ✓ | | |
| Transfer ownership | ✓ | | | |
| Liveshell access | ✓ | ✓ | ✓ | |
| Create API roles | ✓ | ✓ | ✓ | |

> Note: A user's role cannot be changed to `ROOT`. Root users' roles cannot be changed by Admins.

---

## Action Items

### Auth & Settings

- [ ] Decide: document logged-in → `/auth/login` as a known UX quirk, or guard the route with a redirect.
- [x] Sync with Rajput to verify inactivity timeout behaviour when the screen is on sleep.

### Team Settings

- [ ] Add role selector to the Create Invitation dialog — each option needs a label + description.
- [ ] Ensure user type is shown in the invitations table.
- [ ] Enforce role-change restrictions: ROOT-only action, target role cannot be `ROOT`.
- [ ] Restrict Liveshell access to `POWER USER`, `ADMIN`, and `ROOT`.
- [ ] Clarify scope of "develop the power user invite flow" with Rajput.

### Rapid Response View

- [ ] Auto-close the primary sidebar when Query Smith opens.
- [ ] Remove the **Load Query** button; implement click-to-load.
- [ ] Add **Actions** dropdown (load preset / save as preset / go to create query).
- [ ] Add "Save as preset" action to individual query history items.
- [ ] *(Optional)* Multi-select on query history items to batch-save as a preset.

### Misc

- [ ] Update the feature tracking sheet with shipped features.
