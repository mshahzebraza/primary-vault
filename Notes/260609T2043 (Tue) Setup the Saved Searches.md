---
type: "[[Task]]"
categories:
  - "[[Personal]]"
  - "[[Work]]"
  - "[[Tasks]]"
date: 2026-06-12
tags:
  - journal
organization:
  - "[[aiquery.io]]"
projects:
  - "[[aq-client]]"
status: backlog
priority: P2
related-bugs:
---

## Overview
> Save the seached UIs as ASTs in the backgrounds. V1 includes saving the filters only. V2 would mean the integration of sorting. V3 could be the implementation of tags

## Milestones
- [ ] Filter Presets
- [ ] Sort Presets
- [ ] Tags (create and filter)

- [ ] Setup the UI
	- [ ] check how filters button is rendered
- [ ] discussion
	- [ ] inspiration of rapid response history items
	- [ ] toast for the new creation
	- [ ] showing json preview or compact preview for items until the load the detail


## Requirements
- the decision on if the filters sidebar needs to open or not would depend on logic: `anyIsTrue(filterSidebarOpen, savedFilterSidebarOpen`. 
- Then within the Filter Sidebar, if we have the callbacks for both the `setFilters` and `setSavedFilters` then we'd show the 2 tabs version i.e. the `Current`, the default tab, and `Saved` Tabs. Otherwise we show the `v1` version which only had a single view, without any tabs. So basically we'll have a `current-only` as the default and fallback mode, and a new mode of `dual-mode` or `current-and-saved` mode (naming of the modes could be changed to better ones later).
- In the `dual-mode`, when the `Current` tab is shown, then along with the regular `Apply Filters` and `Clear` Button, we also need to show a `Save Filter` Button. This should run the callback of `setSavedFilters` (would probably be named something else like `handleFilterSave`) to save the filter in the api. And based on the response of the API, we show a toast message to the user.
- If API to save the filters is successful, we show the success toast.
- Then the user can switch to `Saved` filters Tab, and view the list of all the saved filters through a `GET` API Call.
- Users are also able to **Delete** a specific saved filter item, by clicking on the delete button on the saved filter item card
- Also, they're able to **Expand** the filter item card (like an accordion) to view the filters content (in a compact format), and choose to either **Load** or **Edit** the filter item.
- If they apply it then the filter would be automatically applied and the tab would automatically change to the `Current` Tab.
- But if they wanted to edit it, then within the expanded area of the card, they'd be able to have the same filter form which they have in the `Current` Tab, but the actions would be different. Instead of `Apply` Button, they'd have the `Save/Update` Button.
	- The Save would trigger the API call but would optimisticaly update the UI, however, in case of failure, would need to show a toast of error. and revert the UI update. 
	- Or could just show a loader in the submit button until the save is completed before updating the UI.
- How the Filters UI going to look like.

### Updated Requirements
- Update Exisitng Action is going to be always be visible that opens a dialog to select the filter-preset which we need to update
- Need to support tags filtering in the filters-v2
- Presets are only going to be supported for the Filters-AST version of filers
- Title and Description would always be required when saving. 
	- Option 1: We can temporarily replace the filter form with a save-as-filter-preset form
	- Option 2: We can show a Form in the footer of the filters panel, just like a checkout section to save it as preset.
- We could put in the tabs to the Right Side of the title header (there's plenty of white space there.)





## Tech Debt
- [ ] Remove the component: `FilterSidebarLayoutTemp` in favor of updated `FilterSidebarLayout` which uses `filterSidebarController` instead of individual `isFilterSidebarOpen` and `toggleFilterSidebar`. Also update all the usage of the `FilterSidebarLayout` component to use the `filterSidebarController` directly.
- [ ] Rename file: `table-filter-formV2.tsx` to `table-filter-form.tsx` and delete the file existing file `table-filter-form.tsx`
- [ ] Analyze the use of `src/components/data-table/dt-filter-form/select-filter-field.tsx` and if it should be deprecated/removed as well as the types/interfaces within it.
- [ ] Analyze the difference between `dt-server-side-search-field-v2.tsx` and `dt-server-side-search-field.tsx` and see if `dt-server-side-search-field-v2.tsx` is usable. If yes, then what is the change across the both versions. Maybe it was intended to accept the `filters` prop without casting `as IServerSideFilters | undefined`.
- [ ] Introduce the React Context for the Data Table components to avoid prop drilling, and use the compound component pattern for it.
- [ ] Why is FilterSidebar not the in same file as TableFilterForm. Why can't they be merged into one.