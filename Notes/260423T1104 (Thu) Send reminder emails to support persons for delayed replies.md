---
type: "[[Task]]"
categories:
  - "[[Work]]"
  - "[[Tasks]]"
organization:
  - "[[scholarbee]]"
projects:
  - "[[sb-backend]]"
status:
  - active
priority: P1
date: 2026-04-23
tags:
  - notifications
  - chat
---

Jira Ticket (**SB-1394**): https://scholarbee-team.atlassian.net/browse/SB-1394

## Overview
Nightly batch (cron at midnight) emails to **all university admins** (including support modeled as a normal uni/campus) who have **unread** student chat messages—not unreplied threads. Copy must state that they have **X unread messages** worth replying to. Reuse existing Scholarbee email layout/components for visual consistency.

## What to build
- **Aggregate** per-admin unread counts efficiently (validate how read/unread is stored per participant: student vs admin).
- **Job** scheduled daily; logging and failure handling; clarify timezone for “midnight.”
- **Template** new content line + inherit shared header/footer/styling from current templates.
- **Edge cases** inactive accounts, large chat tables / heavy batch queries.

## Discovery (before coding)
Confirm in codebase/DB: unread persistence, mark-read API(s) (single vs batch), whether read state is inferred from later messages, and where templates + engine live.

## Current Tasks
- [ ] Phase 1 — map storage, APIs, participant isolation, email template structure
- [ ] Phase 2 — queries, cron wiring, send path, new template, edge cases
- [ ] Updates
	- [ ] Add hard-coded Contact Support Number
	- [ ] Coprights 2024 -> 2026
	- [ ] Add frontend change to handle the redirects mapping (`unread_conversation` -> `chat-page`)
		- Currently, only send to the dashboard page

![[Related Meetings.base]]
