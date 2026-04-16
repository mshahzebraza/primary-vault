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
### Completed Todos
- [x] Create a query-panel UI
- [x] Integrate the query-list hook and add the real query-list navigation
- [x] Add Searching
- [x] Add Collapse button
- [x] Add Resizable Component (dynamic resizing support)
- [x] Add Filter Indicator
### Pending Todos
- [ ] Bug: Moving Across the queries with devics tab selected removes the active-tab state and view returns to default tab i.e. response
- [ ] **Bug:** Filter Sidebar hide animation issue on first filters in query detail view with query list pane
	- when in query detail view with the query list nav pane, go to a fresh query item, apply filters, go to a 2nd fresh query item, you'll notice the filter sidebar suddenly closing.
	- Now come back to 1st query item, and reapply the filters, and now click on other query item, you'll notice the filter sidebar animating to 0 width this time.

### Exploration/Edge Cases

### Implementation Contraints
- Either page level config or the availability of the query pack should decide the rendering of the query-panel. 
- Following variation of query detail pages need to be handled
	- `compliance-assessment-results-query-detail.page.tsx`
	- `query-pack-members-detail.page.tsx`
	- `query-schedule-members-detail.page.tsx`
	- `compliance-qpk-sch-query-detail.page.tsx`
	- `qpk-sch-query-detail.page.tsx`
	- `query-detail.page.tsx`
- since the react router doesn't remount the component, shouldn't we just store the filters in the ref as a map located in the query-detail.view.ts file, and keep updating the map using a callback passed to the children tab components of the query-detail view component.
- the current url-based filtering hook should be kept in use because we want the url-to-maintain-the-current-filter-state
- ***Storage of filters state:*** when url-state setter is used to apply the filters, the filters should also be saved to the local-storage. This can be done in 2 ways. **1) Using an effect that subscribes to the changes in the filter state and syncs the local storage** 2) By calling the local-state setter along with the url-state setter in the same callback. 
- ***Retreival of filters state:*** when the component is mounted, and the url state-setter looks out for the currently applied filters in the url, it should also look for the currently available filters in the local-storage. But prioritize the url-state, and only use the local-storage filters as a fallback. After this initial state retrieval, there should be no other retrieval. Moreover, if the current query-pack-id doesn't match the local-storage-prefix/scope, then delete the previous scope, and start recording the updates in the new scope. Furthermore, since there could be filters stored against multiple queries even for the active query-pack, the initialization should only reset/initlialize the url-filters from local-storage if the local-storage contains the filters against the active-query of active-query-pack. If the filters against the active query aren't avaiable, then let the url filters behave normally; but also no need to clear the other local-storage filters of the other queries of the active query packs
- When should the deletion of previous query-pack-filters scope be carried out. **1) during component mount and filters retrieval.** or 2) during update of filters, at each application
- This is a simplified approach and only disucsses the overall high level flow, the real implementation should also consider the tab specific filters..
