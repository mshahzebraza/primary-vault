---
type:
  - "[[Bug]]"
categories:
  - "[[Work]]"
  - "[[Tasks]]"
organization:
  - "[[scholarbee]]"
projects:
  - "[[sb-backend]]"
status:
  - completed
priority: P2
date: 2026-04-28
jira: "[SB-1227](https://scholarbee-team.atlassian.net/browse/SB-1227)"
---

## Description
> Notifications for recently created/updated admission programs are not being generated in the database.

## Investigations
- Is this a migration issue? Check db for latest notifications for admission programs 
	- attempt to connect the db with cursor and claude

## Steps to Reproduce
1. Create or update an admission program via the CMS
2. Observe that no notification is generated in the DB and no socket messages are emitted

## Root Cause
A `throw new Error("Not Implemented")` had been manually placed at the top of `afterChange_sendNotificationWebhook` as a temporary placeholder. This caused every admission program create/update to silently abort the notification flow — no webhooks were ever fired.

### Pre-existing gap (found during investigation)
The existing guard only checked `if (status === Draft) return`. It had two blind spots:
1. **`receiving_applications` was never checked** — a program explicitly set to `False` would still fire a notification.
2. **`status = Inherit` was not resolved** — if a program inherits its status and the parent admission is still in `Draft`, a notification would still be sent.

## Solution / Fix

### Fix
Removed the `throw` so the hook proceeds to its actual logic.

### Improvement — `isAdmissionProgramNotifiable` utility
Introduced `src/collections/admission-programs/index.utils.ts` with:

- **`resolveEffectiveStatus(programStatus, parentStatus)`** — private helper. Since a program has no `Published` state of its own, `Inherit` always defers to the parent admission session's status.
- **`resolveEffectiveReceivingApplications(programValue, parentValue)`** — private helper. Explicit `True`/`False` on the program win; `Inherit` defers to the parent session.
- **`isAdmissionProgramNotifiable(doc, req)`** — exported async entry point.
  - Fast-exits on `Draft` or explicit `False` without any DB call.
  - Otherwise fetches the parent admission at `depth: 0` (IDs only) and resolves both flags.
  - Returns `true` only when the program is effectively **published AND accepting applications**.

### Bonus — `isAdmissionProgramIndexable` utility
Added a parallel utility for the (currently commented-out) indexing webhook. Indexability is **status-only** — a program should appear in search results even if `receiving_applications` is `False` (visible but not yet open). Same fast-path and parent-fetch pattern, no `receiving_applications` evaluation.

## Conclusion
🐛 _Fix: Admission Program Notifications_ | [SB-1227](https://scholarbee-team.atlassian.net/browse/SB-1227) · [PR #22](https://github.com/Scholarbee-pk/cms-portal/pull/22)

_Issue_ Notifications were not being generated for newly created admission programs. A temporary `throw new Error("Not Implemented")` had been left in the `afterChange` webhook hook, silently blocking all outbound notifications.

_Fix_ Removed the throw so the notification webhook fires correctly on program create/update.

_Optimization_ Replaced the previous simplistic `status === Draft` guard with a proper eligibility check that correctly resolves `inherit` values against the parent admission session: • Programs with `status = inherit` now check whether the parent session is published before firing. • Programs with `receiving_applications = false` are now explicitly excluded. • A lightweight `depth: 0` parent fetch is only triggered when the program document alone isn't enough to determine eligibility — explicit `Draft` and `False` cases fast-exit without any DB call.

A parallel `isAdmissionProgramIndexable` utility was also added (status-only, ignores `receiving_applications`) in preparation for the upcoming auto-indexing webhook.