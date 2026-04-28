---
type: "[[Bug]]"
categories:
  - "[[Work]]"
  - "[[Tasks]]"
date: 2026-04-28
tags:
  - bug
organization:
  - "[[scholarbee]]"
projects:
  - "[[sb-backend]]"
status:
  - completed
priority: P1
jira: "[SB-1227](https://scholarbee-team.atlassian.net/browse/SB-1227)"
related-tasks:
  - "[[260407 (Tue) Emails  Notification regarding missed replies from campus admins to students]]"
---

## Description
> The nightly cron job (`ChatCronService.sendUnreadMessageNotifications`) silently skipped Super Admin users when emitting unread-message emails, even when those users had a valid `campus_id`.

## Root Cause
The MongoDB query in the cron filtered on a single `user_type: "Admin"`. Super Admins store `user_type: "Super_Admin"` — a distinct value — so they never matched and never received emails.

## Solution / Fix

**Bug fix** — Extended the `user_type` filter to include both roles:
```ts
// Before
user_type: UserNS.UserType.Campus_Admin

// After
user_type: { $in: [UserNS.UserType.Campus_Admin, UserNS.UserType.Super_Admin] }
```
`src/chat/chat-cron.service.ts` — only the admin fetch query changed; the rest of the pipeline was untouched.

**Optimization** — Replaced the module-level `sendEmail` utility (`src/utils/mail.config.ts`) — which called `dotenv.config()` at import time and read env vars directly — with an injectable `@Global() EmailService` backed by `ConfigService`. All callers (auth, users, notifications, chat cron) now inject `EmailService` instead.

## Notes
- Cron schedule was temporarily set to `*/5 * * * *` during testing — must be reverted to `EVERY_DAY_AT_MIDNIGHT` before merge.
- Some dev-DB users were temporarily converted to `Student` to isolate a test admin; revert query documented in the PR description.