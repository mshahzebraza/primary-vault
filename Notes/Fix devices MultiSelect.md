---
status: closed
tags:
  - bug
original_path: Notes/Work/aiquery.io/Tasks/Fix devices MultiSelect.md
base: Work
organization: "[[aiquery.io]]"
path_area: Tasks
categories:
  - "[[Work]]"
  - "[[aiquery.io]]"
  - "[[Tasks]]"
---

## Summary
Selected options disappeared from the device multi-select trigger button (pills) when navigating between pages. After the initial fix, a secondary issue emerged where previously selected options couldn't be deselected after pagination.

**PR:** [#380 — fix(ui): preserve selected options across pagination in device multi-select (#374)](https://github.com/AIQuery-Project/client/pull/380)
**Branch:** `fix/shahzeb/374-selected-options-disappear-on-pagination-in-device-multi-select`

## Root Cause
1. **Primary:** The `useEffect` syncing `currentValues` → `selectedOptions` only searched the current page's `allOptionSets`. Options from other pages were filtered out on every page change.
2. **Secondary:** After preserving off-page options, a JS Set reference equality mismatch (`===`) meant `toggleOption` couldn't find preserved options in `selectedValuesSet`, so it tried to re-add them instead of deselecting.

## Fix
- Preserve existing `selectedOptions` that are still in `currentValues` across pagination.
- When navigating back to a page, refresh preserved options with the current page's fresh object references.
- Removed `selectedOptions` from `toggleOption`'s `useCallback` dependency array (redundant — already included via `allOptionsFromAllOptionSetsAndSelectedOptions`).

## Key Learnings
- JS Sets use strict reference equality (`===`) for objects — value equality is not enough.
- Use functional `setState((prev) => ...)` when new state depends on the previous state.
- Redundant `useCallback`/`useMemo` deps cause unnecessary recreations.

## Future Improvements
- Store only primitive values in `selectedValuesSet`; reconstruct option objects on demand.
- Centralised option registry to avoid reference mismatches entirely.

## Files Changed
- `src/components/select-inputs/multi-tab-multi-select-input/multi-tab-multi-select.tsx`
- `src/components/select-inputs/shared/selected-options-pill-set.tsx`
- `src/client/views/create-query/create-query-form/form-components/devices-multi-tab-multi-select.tsx`
