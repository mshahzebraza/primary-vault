---
date: 2026-04-02
attendees: []
categories:
  - "[[Meetings]]"
related-tasks:
  - "[[DashboardWidgets]]"
  - "[[dashboard-&-widgets]]"
type: "[[Meeting]]"
tags:
  - scrum
organization:
  - "[[aiquery.io]]"
---

## Context
Widget creation form requirements and UX decisions.

## Discussion
- Will compatible OS be received in widget data, or requires a separate call to widget template?
- Show disclaimer message of widget compatibility at the top of widget dialog form
- Use the ignore-over-fail strategy for incompatible execution targets for widgets
- Target days will be removed
- Run cadence should only be allowed in creation mode, not in edit mode
- Add a `start-cycle` field (editable in edit mode)
	- For "Day" cadence → DateTime (Default: T + 10min)
	- For "Week" cadence → DateTime (Default: T + 10min)

## Decisions Made
- Use [[Multi Step Form]] with [[stepperize]]
	- https://stepperize.vercel.app/docs/react/api-references/define
	- https://github.com/shadcn-ui/ui/pull/318#issuecomment-2913411946

## Action Items
- [ ] Implement multi-step widget creation form using stepperize
- [ ] Add compatibility disclaimer to widget dialog
- [ ] Remove target days field
- [ ] Lock run cadence to creation mode only
