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

### Plan
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

### Implementation Contraints
- the current url-based filtering hook should be kept in use because we want the url-to-maintain-the-current-filter-state
- Storage of filters state: when url-state setter is used to apply the filters, the filters should also be saved to the local-storage. This can be done in 2 ways. **1) Using an effect that subscribes to the changes in the filter state and syncs the local storage** 2) By calling the local-state setter along with the url-state setter in the same callback. 
- Retreival of filters state: when the component is mounted, and the url state-setter looks out for the currently applied filters in the url, it should also look for the currently available filters in the local-storage. But prioritize the url-state, and only use the local-storage filters as a fallback. After this initial state retrieval, there should be no other retrieval. Moreover, if the current query-pack-id doesn't match the local-storage-prefix/scope, then delete the previous scope, and start recording the updates in the new scope.
- When should the deletion of previous query-pack-filters scope be carried out. **1) during component mount and filters retrieval.** or 2) during update of filters, at each application
### Pseudocode implmentation:

```tsx title:"use-query-response.v2.hook.tsx"

const LS_KEY = 'special-query-response-v2-filters'
const useQueryResponseViewHookV2 = (props: IQueryResponseViewHookProps) => {
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
			setLsFilters(newFiltersState)
		}
	});
	
	// Update Option 2: useEffect to sync the url filters with the ls-filters
	const filtersRef=useRef(filters)
	useEffect(()=>{
		setLsFilters(filtersRef.current)
	},[filtersRef.current])
	
	
	// Initialization Option 2: useEffect on mount to set the url-filters using local-storage filters state
	useEffect(()=>{
		// if filters are not applied, load the filters from the local storage
		if (!filters && lsFilters) setFilters(lsFilters)
	},[])
}
	


```



![[Related Meetings.base]]

## 2026-04-10
