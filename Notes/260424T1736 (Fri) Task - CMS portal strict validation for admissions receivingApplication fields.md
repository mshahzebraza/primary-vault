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
status: backlog
priority: P1
date: 2026-04-24
tags:
  - backend
  - admissions
  - validation
  - portal
---

## Overview
> Add strict validation in the CMS portal for admission/admission-program properties: admission start/end dates, status, and receiving-application related fields.

Prevent setting a “receiving application plan” for an admission/admission program whose `receivingApplication` is `false`.

## Current Tasks
- [ ] Identify all CMS portal endpoints/flows that create or update:
  - [ ] admission start/end date
  - [ ] status flag
  - [ ] `receivingApplication`
  - [ ] receiving application plan/value
- [ ] Add strict server-side validation:
  - [ ] reject invalid or inconsistent date ranges
  - [ ] validate status flag is present and consistent with allowed transitions (as per existing domain rules)
  - [ ] if `receivingApplication=false`, reject any attempt to set receiving application plan
- [ ] Add regression tests for the portal validation rules (including “toggle receivingApplication to false then plan must be unset” scenarios).
- [ ] Ensure error responses are actionable (field-level validation errors where possible).

## Acceptance Criteria
- [ ] CMS portal rejects inconsistent admission/admission-program state updates.
- [ ] Receiving application plan cannot be set when `receivingApplication=false` (create and update paths).
- [ ] Tests cover key edge cases and prevent regressions.

![[Related Meetings.base]]
