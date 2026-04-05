---
status: open
tags:
- bug
aliases:
- 'Bug: Momentary "No data found" Flash in Query Results Table'
organization: '[[aiquery.io]]'
categories:
- '[[Work]]'
- '[[aiquery.io]]'
- '[[Tasks]]'
type: '[[Bug]]'
projects: []
priority: P2
---
## Description
On the Custom Extension testing tab, on subsequent query runs (not the first), the table briefly flashes "No data found for this query" before the loading spinner appears.

**Location:** `src/client/views/create-custom-extension/create-custom-extension-form/steps/testing/sections/query-results/use-query-results.hook.tsx`

## Root Cause
```
1. User clicks "Run Query" → onRunQuerySuccess() resets isQueryResponseDataFetchEnabled = false
2. shouldEnableQueryResponseDataListFetchQuery = arePreviousStepsEnabled && isQueryResponseDataFetchEnabled → false
3. React Query returns CACHED data (enabled=false, no new fetch)
4. Cached data has isFetching=false, isFetched=true
5. Loading check: shouldEnableQueryResponseDataListFetchQuery && isFetching → false
6. Table renders cached/empty state ("No data found") briefly
7. Later: query-response completes → isQueryResponseDataFetchEnabled=true → new fetch starts → spinner shows
```

## Attempted Fixes (did not resolve)
- `!isFetched` instead of `isFetching` — same issue, `shouldEnable...` is still false
- `!isActiveQueryResponseSuccessful` — stale cached response still has `success=true`
- `isQueryResponsePolling` — polling state also affected by stale cache timing

## Potential Solutions
1. Cache invalidation — call `queryClient.invalidateQueries()` or `removeQuery()` on new query run
2. Dedicated waiting state — add `isWaitingForNewData` boolean, set on query start, cleared on data arrival
3. Dynamic query key — append unique ID to query key that changes on each run
4. `placeholderData: keepPreviousData` — maintain previous data during transition instead of showing empty state

## Related Notes
- [[custom extension bugs]]
