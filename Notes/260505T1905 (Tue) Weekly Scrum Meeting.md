---
type: "[[Meeting]]"
categories:
  - "[[Personal]]"
  - "[[Meetings]]"
date: 2026-05-05
tags:
  - journal
organization:
projects: []
attendees: []
---

## Context
> Brief note on why this meeting happened / what triggered it.

## Discussion
- Sheet to update based on the features
- document in codebase the UX issue that user when logged in can go to the login page again
	- Either document that its a minor UX issue, and not an issue
	- OR guard it to not show up when user navigates to `auth/login` through URL while he is logged out 
- Not Confirmed: if screen is on sleep, the inactivity timeout doesn't logout the user.
	- sync with Rajput to discuss the working of inactivity timeout

## Decisions Made

## Action Items
- [ ] 