---
type: "[[Task]]"
categories:
  - "[[Work]]"
date: 2026-04-10
tags:
  - feature
organization:
  - "[[aiquery.io]]"
projects:
  - "[[aq-client]]"
status:
  - active
priority: P2
---

## Overview
> One paragraph describing what and why.

## Todos
### Completed

^856908

- [x] Create a query-panel UI
- [x] Integrate the query-list hook and add the real query-list navigation
- [x] Add Searching
- [x] Add Collapse button
- [x] Add Resizable Component (dynamic resizing support)
- [x] Add Filter Indicator
### Pending 

- [ ] Bug: Moving Across the queries with devics tab selected removes the active-tab state and view returns to default tab i.e. response
- [ ] **Bug:** Filter Sidebar hide animation issue on first filters in query detail view with query list pane
	- when in query detail view with the query list nav pane, go to a fresh query item, apply filters, go to a 2nd fresh query item, you'll notice the filter sidebar suddenly closing.
	- Now come back to 1st query item, and reapply the filters, and now click on other query item, you'll notice the filter sidebar animating to 0 width this time.
