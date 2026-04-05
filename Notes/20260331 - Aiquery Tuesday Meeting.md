---
date: 2026-03-31
attendees: []
related:
  - "[[DashboardWidgets]]"
tasks: "[[dashboard-&-widgets]]"
original_path: Notes/20260331 - Aiquery Tuesday Meeting.md
base: NotesRoot
categories:
  - "[[NotesRoot]]"
  - "[[Meetings]]"
---

## Context
Weekly Tuesday sync — dashboard UX overhaul decisions.

## Discussion

### Dashboard renaming & UX changes
- Rename Dashboard Section/Collection → Dashboard Tab
- Move the edit button into edit layout mode
- Remove the maximize button from the main view
- Move export data and query results into the Widget Detail Dialog
- Remove the export data button from the main dashboard toolbar
- Rename section actions: "Edit Title", "Delete Section"
- Rename sections/collections → dashboard tabs throughout the UI
- Add an "Add" button to toolbar actions in edit layout mode
- Add an edit button to individual widgets in edit layout mode
- Rename "Edit Layout" → "Edit Mode"
- UI accent: something purple

### Tech tasks surfaced
- Investigate query cache invalidation on dashboard update/delete hooks — may be too intensive
- Use promise-to-resolved toast pattern for dashboard update/delete API calls

## Decisions Made
- Sections → Tabs (rename everywhere)
- Edit Layout → Edit Mode

## Action Items
- [ ] Implement all renaming changes
- [x] Move export data + query results into Widget Detail Dialog
- [x] Review cache invalidation on dashboard hooks
- [ ] Switch dashboard mutation calls to promise-to-resolved toast pattern
