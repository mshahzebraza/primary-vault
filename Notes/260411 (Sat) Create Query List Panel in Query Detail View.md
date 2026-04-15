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

## Current Tasks
- [ ] Create a [[#Plan|plan for the implementation]]
- [x] Create a query-panel UI
- [ ] Integrate the query-list hook and add the real query-list navigation
- [ ] How to keep the filters intact for the query detail.
	- The query click is supposed to change the query-param in the url, which *might* always trigger the new page mount, causing the state to be lost for the view. *Please confirm this...*
	- If this unmount is inevitable, should we keep the filters in the local storage somewhere?
		- yes, and replace the local storage of the previous query-pack with the current one.
- Quality of life improvements
	- [ ] Add Searching
	- [ ] Add Collapse button
	- [ ] Add Resizable Component (dynamic resizing support)
- [ ] Perform the refactoring mentioned in the `src/client/views/query-detail/query-detail.view.tsx` related to the query list hook
- [ ] TODOs
	- [ ] if filter-1 is applied on query-1, and we switch to query-b, then fitler sidebar closes, filter-1 is removed from both the url, and the local-storage, and if we come back to query-1, we would see unfiltered data. filter sidebar closing is expected, but no retrieval of applied filter-1, when coming back to query-1 is also unexpected.
	- [ ] Now apply filter-1 on query-1, and go back to query-2 again, this time filter sidebar doesn't close this time, but the url filters state is removed from url. However, the query-2 results now have the filter-1 applied, which is also seen in the local storage i.e. the same filter-1 is not mapped to the query-2 as well along with query-1. The sidebar staying open even after navigation, the filters-1 being applied to query-2 and copied to the query-2 mapping in local-storage, both are unexpected behaviors.
	- [ ] It appears that this behavior continues on with subsequent queries as well such that, each time we visit a fresh query from the query-panel, the filter state is removed, the sidebar is closed, and even the local storage filters are purged. But if filter is applied and a previously selected/navigated query is chosen, the filters stay applied even for the changed query and sidebar stays open, until a fresh query is opened, or filters are purged/cleared manually

	- [ ] then all the queries which have been visited earlier, would keep the filter sidebar opened, the filter-1 would stay applied, however, the filter

### Exploration/Edge Cases
- Either page level config or the availability of the query pack should decide the rendering of the query-panel. 
- Following variation of query detail pages need to be handled
```
compliance-assessment-results-query-detail.page.tsx
query-pack-members-detail.page.tsx
query-schedule-members-detail.page.tsx
compliance-qpk-sch-query-detail.page.tsx
qpk-sch-query-detail.page.tsx
query-detail.page.tsx
```
- since the react router doesn't remount the component, shouldn't we just store the filters in the ref as a map located in the query-detail.view.ts file, and keep updating the map using a callback passed to the children tab components of the query-detail view component.
## Acceptance Critera
- [ ] `qpk_1:qry_1:response` => `qpk_1` => `qpk_1:qry_1:response` navigation reset filters for Query-Detail View
- [x] retreive ls-filters on initialization
	- ✅ Effect based
	- Init Callback Based
- [x] save ls-filters on url-filters update
	- ✅ Effect based on url-filters change (selected option)
	- Success Non-Empty Response Effect Based
	- Parallel Callback Based
### Implementation Contraints
- the current url-based filtering hook should be kept in use because we want the url-to-maintain-the-current-filter-state
- ***Storage of filters state:*** when url-state setter is used to apply the filters, the filters should also be saved to the local-storage. This can be done in 2 ways. **1) Using an effect that subscribes to the changes in the filter state and syncs the local storage** 2) By calling the local-state setter along with the url-state setter in the same callback. 
- ***Retreival of filters state:*** when the component is mounted, and the url state-setter looks out for the currently applied filters in the url, it should also look for the currently available filters in the local-storage. But prioritize the url-state, and only use the local-storage filters as a fallback. After this initial state retrieval, there should be no other retrieval. Moreover, if the current query-pack-id doesn't match the local-storage-prefix/scope, then delete the previous scope, and start recording the updates in the new scope. Furthermore, since there could be filters stored against multiple queries even for the active query-pack, the initialization should only reset/initlialize the url-filters from local-storage if the local-storage contains the filters against the active-query of active-query-pack. If the filters against the active query aren't avaiable, then let the url filters behave normally; but also no need to clear the other local-storage filters of the other queries of the active query packs
- When should the deletion of previous query-pack-filters scope be carried out. **1) during component mount and filters retrieval.** or 2) during update of filters, at each application
- This is a simplified approach and only disucsses the overall high level flow, the real implementation should also consider the tab specific filters..
### Pseudocode implmentation:

```tsx title:"use-query-response.v2.hook.tsx"

const LS_KEY = 'special-query-response-v2-filters'
const useQueryResponseViewHookV2 = (props: IQueryResponseViewHookProps) => {

	// create the LS_FITLERS_KEY with the help of props
	const LS_FILTERS_KEY = `<qpk_id>:<qry_id>`
	const {lsFilters, setLsFilters} = useLocalStorageFilters(LS_KEY)


	// TODO: This should be either updated or combined with custom code to store and load local-storage
	const { filters, setFilters, resetFilters } = useManualFiltersV2({
		
		// Initialization Option 1: initialize the filters through lsFilters if filters are not available in the url
		// the hook should internally handle the fallback usage of lsFilters in the initialization phase. This approach might save us the side effect, but will make the hook more complex i.e. additional handling of lsFiltersInitialization is added only for this use-case
		lsFiltersForInitialization: lsFilters
			
		// OLD IMPLEMENTATION
		// onFilterChange: resetPagination
		// NEW IMPLEMENTATION
		onFilterChange: (newFiltersState)=>{
			resetPagination()
			// Update Option 1: also update local-storage filters
			setLsFilters(LS_FILTERS_KEY, newFiltersState)
		}
	});
	
	// Update Option 2: useEffect to sync the url filters with the ls-filters
	const filtersRef=useRef(filters)
	useEffect(()=>{
		setLsFilters(LS_FILTES_KEY, filtersRef.current)
	},[filtersRef.current])
	
	
	// Initialization Option 2: useEffect on mount to set the url-filters using local-storage filters state
	useEffect(()=>{
		// if filters are not applied, load the filters from the local storage
		// But ensure that the loaded filters are of the current query. 
		if (!filters && lsFilters[LS_FILTERS_KEY]) setFilters(lsFilters)
	},[])
}
```



## Todos


![[Related Meetings.base]]

## 2026-04-10


## Timeline
- React Router Based Nuqs Adaptor Issue
- Misunderstanding that React Router remounts component. It actually rerenders the same component like a usual prop change
- local-storage schema update