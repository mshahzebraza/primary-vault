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
- [x] Validate permissions + error states (e.g. disconnected agents) and copy.
- [x] The agent groups shown in the dropdown must be restricted only to the static agent groups. Update the agent group device selection form field if required to support the group type filters
- [x] Add a "Remove Agents" action for agent list views bulk actions and ensure refetching afterwards.
- [x] BUG: Confirm refetch on removal-from-agent is working
- [ ] Ensure the bulk and individual actions to add the agents to group are available in all the variations of the agent list views
- [ ] Optional: Omit the current AgentGroup from the Target AgentGroup selection list
	- [ ] Allow the render callback to in the DeviceGroupFormField component, and use it to custom render the dropdown item component for the existing agent group.
- [ ] Add a CTA for the toast to go to the agent group page where the agents are added.
- [x] Feat: Create a Single-Value-SelectFormField for the device agent group selection
- [ ] Detect the view of dynamic agents and disable the "Remove from Group" button in that view as removal from dynamic agents cannot be controlled.
- [ ] Keep the deletion actions at the last in the bulk actions dropdown for agent list view.
- [ ] Refactor the agent list variations like query list view.

## Potential Tasks
- [ ] In agent group view, add other agents into the current agent group.
- [ ] 


![[Related Meetings.base]]
