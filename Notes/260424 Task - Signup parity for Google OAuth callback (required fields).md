---
type:
  - "[[Task]]"
categories:
  - "[[Work]]"
  - "[[Tasks]]"
organization:
  - "[[scholarbee]]"
projects:
  - "[[sb-frontend-student]]"
  - "[[sb-backend]]"
status: backlog
priority: P1
date: 2026-04-24
tags:
  - frontend
  - backend
  - auth
---

## Overview
> Ensure the required fields for standard signup remain **required** for Google OAuth signup as well.

The student frontend should intercept the Google callback and enforce missing required information collection before completing account creation.

## Current Tasks
- [ ] Identify the canonical “required signup fields” contract (backend DTO/schema + frontend form requirements).
- [ ] Update Google OAuth callback handling in `sb-frontend-student` to block completion when required fields are missing and route user to completion flow.
- [ ] Ensure backend rejects incomplete Google signup payloads the same way it rejects normal signup payloads (no “OAuth bypass”).
- [ ] Add/update API + UI tests for:
  - [ ] normal signup still requires fields
  - [ ] Google signup still requires same fields
  - [ ] partial completion/resume behavior on callback

## Acceptance Criteria
- [ ] A user cannot complete Google signup without providing the same required information as normal signup.
- [ ] Frontend intercepts OAuth callback and presents a completion flow (no “silent success”).
- [ ] Backend validation is consistent across both signup paths.

![[Related Meetings.base]]
