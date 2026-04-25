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
status: backlog
priority: P2
---

## Overview
> **Bug Bash ID 45** - There is currently no way to add agents to an existing **static group** in the UI. After a static group is created, there's no UI path to add more agents unless you do it during install/onboarding.

## Current Tasks
- [ ] Add an "Add agents" entry point for existing static groups (post-create).
- [ ] Ensure selection/search UX supports scaling to many agents.
- [ ] Validate permissions + error states (e.g. disconnected agents) and copy.
- [ ] Ensure the bulk and individual actions are shown only in the static agent group member list view
- [ ] The agent groups shown in the dropdown must be restricted only to the static agent groups. Update the agent group device selection form field if required to support the group type filters
- [ ] Optional: Omit the current AgentGroup from the Target AgentGroup selection list
- [ ] Add a "Remove Agents" action for agent list views bulk actions and ensure refetching afterwards.
- [ ] Add a CTA to go to the agent group page where the agents are added.
- [ ] BUG: Confirm refetch on deletion is working
- [ ] Feat: Create a Single-Value-SelectFormField for the device agent group selection
- [ ] Detect the view of dynamic agents and disable the "Remove from Group" button in that view as removal from dynamic agents cannot be controlled.
- [ ] Keep the deletion actions at the last in the bulk actions dropdown for agent list view.
- [ ] Refactor the agent list variations like query list view.


![[Related Meetings.base]]
