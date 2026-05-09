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
related-tasks:
  - "[[260509T1213 (Sat) Task - Rapid Response View Enhancements]]"
  - "[[260505 (Tue) Task - Team Settings & Role Management]]"
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

→ [[260505 (Tue) Task - Team Settings & Role Management]]

### Rapid Response View

→ [[260509T1213 (Sat) Task - Rapid Response View Enhancements]]

---

## Action Items

### Auth & Settings

- [ ] Decide: document logged-in → `/auth/login` as a known UX quirk, or guard the route with a redirect.
- [x] Sync with Rajput to verify inactivity timeout behaviour when the screen is on sleep.

### Team Settings

→ [[260505 (Tue) Task - Team Settings & Role Management#Tasks]]

### Rapid Response View

- [x] Auto-close the primary sidebar when Query Smith opens.
- [x] Remove the **Load Query** button; implement click-to-load.
- [ ] Remaining items → [[260509T1213 (Sat) Task - Rapid Response View Enhancements]]

### Misc

- [ ] Update the feature tracking sheet with shipped features.
