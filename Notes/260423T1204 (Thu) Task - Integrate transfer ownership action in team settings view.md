---
type: "[[Task]]"
categories:
  - "[[Work]]"
  - "[[Tasks]]"
date: 2026-04-23
tags:
  - ui
  - settings
  - team
organization:
  - "[[aiquery.io]]"
projects:
  - "[[aq-client]]"
status:
  - active
priority: P1
---

## Overview
Integrate **Transfer Ownership** action in **Settings → Team** with an explicit **confirm dialog** and clear UX states (loading/success/error).

## Requirements
- **UI entry point**: add “Transfer ownership” action in the Team Settings view.
- **Confirmation**: modal/dialog requiring explicit confirmation before executing.
- **Request**: call `/{domain}/tenant/transfer-ownership` with body `{ newRootUserId: string }`.
- **UX**: disable confirm while pending; show success + failure messaging; keep user list refreshed if needed.

## Current Tasks
- [x] Locate current Team Settings actions + patterns for confirm dialogs
- [x] Wire action → API call → toast/feedback + refresh
- [x] QA: permission constraints (root/admin only), self-transfer prevention, error states

## Follow-ups / Bugs found post-integration
- [x] **False failure shown after successful transfer (response validation failing)**
	- Root cause: client-side validation of transfer ownership API response fails → mutation treats it as API failure
	- Status: fixed locally on minor-tasks branch (not pushed yet)
	- [x] Ensure the response schema/validation matches the real API contract (or relax to tolerate extra/missing fields safely)
- [x] **Roles not updating in Team Settings view after successful transfer (even after refresh memberships)**
	- **Symptom**: After “Transfer ownership”, the memberships `GET` fired while the transfer `POST` was still in-flight, so the refetch often returned the old roles (root/user didn’t swap in the UI).
	- **Root cause**: The React Query mutation wasn’t actually awaiting the transfer `POST`. We wrapped the async call with `sonnerToast.promise(...)`, but forgot to chain `.unwrap()` — without that, the mutation path didn’t reliably await the underlying network promise, so React Query treated the mutation as “done” early and kicked off the refetch in parallel with the `POST`.
	- **Fix**: Make the mutation return something awaitable tied to the underlying `POST` (final working version: `toast.promise(...).unwrap()`), so the `GET` only starts after the `POST` resolves (matches Network inspector sequencing).
	- [x] Verify the memberships refresh actually invalidates the right query keys / state slices *(not the real issue once sequencing was fixed)*
	- [x] Confirm server returns updated roles for current user immediately after transfer *(was masked by parallel refetch timing)*
	- [x] Fix UI state so the view reflects updated roles without requiring a hard reload / navigation away *(fixed by awaiting the transfer correctly)*


![[Related Meetings.base]]
