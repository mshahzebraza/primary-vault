---
status: active
tags:
- task
- RnD
organization: '[[aiquery.io]]'
categories:
- '[[Work]]'
- '[[aiquery.io]]'
- '[[Tasks]]'
type: '[[Task]]'
projects: []
priority: P2
---

## Overview
Adding debouncing to the table search input without breaking the existing filter state sync.

## Prior Implementation (how it worked before)
- `primary-search-field` key extracted from column definition; only one primary key per table
- `filters.regex` state used as the search value
- Search input handler directly updated `filters` state on every keystroke (same state powering the sidebar)
- On each update: if empty → remove all filters on `primary-search-field`; if valid → apply `regex` filter (remove `eq`, `in`, `neq` etc.)

## Debounced Implementation (current state)
- Derived state from `filters[primary-search-field].regex` stored in a local `useState`
	- _Why a new state and not derived state? — Needed to reflect UI updates in real-time while the actual filter state update is delayed_
- Effect on mount sets `setSearchInputValue` to the initial filter value

## Open Architecture Questions
- **Filter ownership:** Should the search input override only its own `primary-search-field` filters, or reset all view-level filters?
	- Current: overrides `primary-search-field` filters, keeps others — but this forces search to stay in sync with view-level filters and makes debouncing harder
- **Decoupling option:** Can API calls be triggered directly from search input state instead of going through `setFilters`? This would remove the need for a `useEffect` to sync debounced value → filters state
	- Could we enforce mutual exclusivity: using search clears advanced filters and vice versa (clean-slate approach)?
	- Or use `useDebouncedCallback` directly on the `setFilters` updater to avoid extra effects?

## Related Notes
- [[Filtering Optimization]]
- [[Tasks Manifest - Ai Query]]
