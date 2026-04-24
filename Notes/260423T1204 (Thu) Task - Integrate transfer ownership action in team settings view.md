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


![[Related Meetings.base]]
