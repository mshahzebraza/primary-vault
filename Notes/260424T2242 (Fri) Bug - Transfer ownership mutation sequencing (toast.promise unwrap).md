---
type: "[[Task]]"
categories:
  - "[[Work]]"
  - "[[Tasks]]"
date: 2026-04-24
tags:
  - ui
  - settings
  - team
  - bug
  - react-query
organization:
  - "[[aiquery.io]]"
projects:
  - "[[aq-client]]"
status:
  - completed
priority: P2
parent-task: "[[260423T1204 (Thu) Task - Integrate transfer ownership action in team settings view]]"
---

## Overview
Fix the **roles not updating** after transfer ownership caused by the mutation finishing early due to a non-awaitable `toast.promise(...)` wrapper. Ensure the memberships refetch happens **after** the transfer `POST` resolves by using `toast.promise(...).unwrap()`.

## Summary of the fiasco
- **Symptom**: After “Transfer ownership”, the memberships `GET` fired while the transfer `POST` was still in-flight, so the refetch often returned the old roles (root/user didn’t swap in the UI).
- **Root cause**: React Query mutation was not actually awaiting the transfer `POST`. Wrapping with `sonnerToast.promise(...)` without chaining `.unwrap()` meant the mutation didn’t reliably await the underlying network promise, causing the refetch to run in parallel.
- **Fix**: Return an awaitable promise tied to the `POST` (final working version: `toast.promise(...).unwrap()`), so the `GET` starts only after the `POST` resolves (matches the Network inspector).

## Current Tasks
- [x] Make mutation return an awaitable tied to the underlying transfer `POST` (`toast.promise(...).unwrap()`).
- [x] Verify the memberships refetch starts only after transfer `POST` resolves (Network inspector).
- [x] Confirm roles update correctly in Team Settings view without requiring a hard reload.

## Done Criteria
- [x] Transfer `POST` completes before memberships `GET` refetch is triggered.
- [x] UI reflects updated roles immediately after transfer.

![[Related Meetings.base]]
