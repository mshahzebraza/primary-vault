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
  - "[[sb-frontend-student]]"
status: backlog
priority: P2
date: 2026-04-24
tags:
  - backend
  - frontend
  - admissions
  - filtering
---

## Overview
> Offload “admission status” derivation to the frontend.

Backend should only accept **value-based filters**; frontend derives UI states (e.g. `openSoon`, `closingSoon`, etc.) from raw values (dates/flags/status).

## Current Tasks
- [ ] Define the backend “value-based filter” contract (allowed filter keys + allowed values) and remove/avoid derived-state filters.
- [ ] Update backend filtering to accept only value-based filters (no derived enums like `openSoon`).
- [ ] Implement frontend derivation helpers for UI states (`openSoon`, `closingSoon`, etc.) using admission start/end dates + status flags + receiving-application flag.
- [ ] Ensure frontend uses derived states only for presentation, not as backend query params.
- [ ] Add regression tests:
  - [ ] backend filter validation (reject derived-state filters)
  - [ ] frontend derived-state mapping across edge cases (missing dates, boundary dates, status=false, receivingApplication=false)

## Acceptance Criteria
- [ ] Backend filtering only uses value-based filters and rejects derived “status buckets”.
- [ ] Frontend consistently derives and displays admission state labels from raw values.
- [ ] Existing listing/search UX remains correct (no loss of filtering capability).

![[Related Meetings.base]]
