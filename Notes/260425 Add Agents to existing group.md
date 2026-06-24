---
type: "[[Task]]"
categories:
  - "[[Work]]"
  - "[[Tasks]]"
date: 2026-04-25
tags:
  - journal
organization:
  - "[[aiquery.io]]"
projects:
  - "[[aq-client]]"
status:
  - completed
priority: P2
---

## Overview
> **Bug Bash ID 45** - There is currently no way to add agents to an existing **static group** in the UI. After a static group is created, there's no UI path to add more agents unless you do it during install/onboarding.

## Current Tasks
- [x] Validate permissions + error states (e.g. disconnected agents) and copy.
- [x] The agent groups shown in the dropdown must be restricted only to the static agent groups. Update the agent group device selection form field if required to support the group type filters
- [x] Add a "Remove Agents" action for agent list views bulk actions and ensure refetching afterwards.
- [x] BUG: Confirm refetch on removal-from-agent is working

- [x] Feat: Create a Single-Value-SelectFormField for the device agent group selection
- [ ] Optional: Add a CTA for the toast to go to the agent group page where the agents are added.



![[Related Meetings.base]]
