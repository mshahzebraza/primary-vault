---
type: "[[Bug]]"
categories:
  - "[[Personal]]"
  - "[[Work]]"
  - "[[Tasks]]"
date: 2026-04-28
tags:
  - journal
  - bug
organization:
  - "[[scholarbee]]"
projects:
  - "[[sb-backend]]"
status:
  - backlog
priority: P1
related-tasks:
  - "[[260407 (Tue) Emails  Notification regarding missed replies from campus admins to students]]"
---

## Description
> What is the symptom? Where does it happen?

**Location:** 

## Steps to Reproduce
1. 

## Root Cause

## Attempted Fixes

## Solution / Fix

## Notes


## Conclusion
**[SB-1227] Fix: Missed replies — unread message emails not reaching all admins** 🔗 Jira: [https://scholarbee-team.atlassian.net/browse/SB-1227](https://scholarbee-team.atlassian.net/browse/SB-1227) 🔗 PR: _(add link after opening)_

**Issue** Campus admins were receiving unread message notification emails, but Super Admins with a valid `campus_id` were being silently excluded. The cron query filtered strictly on `user_type: "Admin"`, so Super Admin users never matched.

**Fix** Extended the user query to include both `Campus_Admin` and `Super_Admin` user types, so all admin roles associated with a campus now receive the daily digest.

**Optimization** Replaced the module-level `sendEmail` utility (which read `RESEND_API_KEY` and `DEFAULT_FROM_EMAIL` directly from `process.env`) with an injectable `EmailService` backed by NestJS `ConfigService`. This aligns email config with the rest of the app's typed config layer, removes the `dotenv.config()` side-effect at import time, and centralises the default-sender fallback in one place for all callers (auth, users, notifications, chat cron).