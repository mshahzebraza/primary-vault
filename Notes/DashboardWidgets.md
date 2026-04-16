---
status:
  - blocked
tags:
  - feature
organization: "[[aiquery.io]]"
categories:
  - "[[Work]]"
  - "[[Tasks]]"
type: "[[Task]]"
projects:
  - "[[aq-client]]"
priority: P2
---

## Overview
Dashboard/Widget system — creation, layout, and detail view for widgets on dashboards.

## 2026-04-02 (Widget Creation meeting decisions)
- Use [[Multi Step Form]] with [[stepperize]] for widget creation form
	- https://stepperize.vercel.app/docs/react/api-references/define
- Show compatibility disclaimer at top of widget dialog form
- Ignore-over-fail strategy for incompatible execution targets
- [x] Remove target days field
- [x] Run cadence: creation mode only (not editable in edit mode)
- [x] Add `start-cycle` field (editable in edit mode)
	- Day cadence → DateTime (default: T + 10min)
	- Week cadence → DateTime (default: T + 10min)

## 2026-03-31 (Tuesday meeting decisions)
- [ ] Rename sections/collections → Dashboard Tabs everywhere
- [ ] Rename "Edit Layout" → "Edit Mode"
- [x] Move edit button into edit mode toolbar
- ~~Remove the maximize button~~ → add back maximize button for widget detail (see 24-March below)
- [ ] Move export data + query results into Widget Detail Dialog
- [ ] Remove export data button from main dashboard toolbar
- [ ] Rename section actions: "Edit Title", "Delete Section"
- [x] Add "Add" button to toolbar in edit layout mode
- [x] Add edit button to individual widgets in edit layout mode
- [ ] Use promise-to-resolved toast pattern for dashboard mutations

## 2026-03-24
- [x] Delete Widget button shown in edit layout mode — fix visibility
- [x] Put view/tab actions in the view-content area
- [x] Add back the maximize button for widget detail
- [x] Dropdown goes away completely — query results + export data go into detail view
- Add subtitle showing date range (below widget title)
- Add date range selection in widget detail view dialog

## Current Tasks

- [ ] Enhance multi-step widget creation
	- [x] Implement multi-step widget creation form (stepperize)
	- [ ] Use Stepperize
- [x] Widget compatibility disclaimer in dialog
- [x] Remove target days, lock run cadence to creation
- [x] Add start-cycle field
- [x] Use [Time Component from shadcn](https://ui.shadcn.com/docs/components/radix/date-picker#time-picker) instead of custom functionality
- [x] Rename all sections → tabs, Edit Layout → Edit Mode
- [x] Move export data + query results into Widget Detail Dialog
- [x] Add Add/Edit buttons to toolbar and individual widgets in edit mode
- [x] Fix Delete Widget button visibility (edit mode only)
- [x] Add date range subtitle in widget detail dialog
	- Query: We currently get the data for all the widgets in the dashboard-tab in one api request. If that stays valid, then how'd we be able to fetch the specific widgets' data for a specific time-frame. Because that'd require either (1) a widget specific request + merging of query-cache with the `section-widgets` API, or (2) we re-fetch the `section-widgets` API with a filter object like `{widget_1: ["2026-01-10","2026-01-10" ]}`
- [x] inherit & overridden flag for widget
- [x] choose widgets from inventory (frequency, type)
- [x] each widget links to full details
- [x] dashboard creation = title + tags only
- [x] tags input for dashboard tab creation
- [x] fix UX issues on dialog buttons and accessibility
- [x] Add Widget Detail Dialog (with Tabs, AI Summary, Footer with Follow-ups)
- [x] make execution target specific to tabs, not dashboard
- [x] review cache invalidation intensity on dashboard hooks
- [ ] switch dashboard mutations to promise-to-resolved toast pattern

## Resources
- https://react-grid-layout.github.io/react-grid-layout/examples/01-basic.html

## Related Meetings
- [[202604022216 - Widget Creation meeting]]
- [[20260331 - Aiquery Tuesday Meeting]]
