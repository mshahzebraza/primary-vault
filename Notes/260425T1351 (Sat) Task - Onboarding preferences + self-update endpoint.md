---
type:
  - "[[Task]]"
categories:
  - "[[Work]]"
  - "[[Tasks]]"
organization:
  - "[[scholarbee]]"
projects:
  - "[[sb-backend]]"
status: completed
priority: P2
date: 2026-04-25
tags:
  - backend
  - onboarding
  - users
---

## Overview
> Capture structured onboarding signals for personalization, and make “update my profile” safer and simpler.

During onboarding, we need to store a user’s preferences in a consistent, structured way so downstream recommendations can use them reliably. In parallel, introduce a self-update path that updates the currently authenticated user without requiring a user ID in the URL, and mark the older “update by ID” path as deprecated.

## Current Tasks
- [x] Add a structured place to store onboarding preference information on the user profile.
- [x] Support partial updates so users can update one preference without overwriting the rest.
- [x] Ensure “clear/opt-out” behavior is supported where applicable.
- [x] Add a “self-update” endpoint that targets the authenticated user.
- [x] Deprecate the legacy “update user by ID” endpoint (keep it working for now).
- [x] Keep API documentation aligned across both update paths.
- [x] Add validation and tests to prevent invalid ranges and ensure update semantics remain consistent.

## Acceptance Criteria
- [x] Onboarding preference data can be saved and updated incrementally without unexpected overwrites.
- [x] Users can clear/opt-out of preference data intentionally.
- [x] Authenticated users can update their own profile via the preferred self-update endpoint.
- [x] The legacy update-by-ID endpoint remains available but is clearly marked as deprecated.
- [x] Invalid inputs (e.g., inconsistent ranges) are rejected consistently.

![[Related Meetings.base]]
