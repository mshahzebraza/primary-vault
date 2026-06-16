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
> Save the seached UIs as ASTs in the backgrounds. V1 includes saving the filters only.  V2 would mean the integration of sorting. V3 could be the implementation of tags

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

## Tasks
Here is the list of out-of-scope enhancement tasks:

1. **Case-Sensitivity:** Add case-sensitivity toggles directly within the filters UI.
2. **Collapsible Rules:** Allow inactive filter rules or items to collapse into a compact preview mode, expanding into full cards only when active or clicked. This will improve readability and save screen space.
3. **Undo Button:** Re-add the "Undo" button (either at the top of the filters panel or within the actions panel at the bottom).
4. **Icons & Tooltips:** * Use specific "filter plus" and "layers plus" icons for the "Add Condition" and "Add Subgroup" actions.
   * Add dedicated action icons for "Undo" and "Clear Filters".
   * Add descriptive tooltips (e.g., "Remove group", "Remove filter rule") to all close/cross (X) buttons.
5. **Tag Selection UX:** Automatically default to the "has key-value pair" option when "tags" is selected in the column dropdown, removing the redundant manual step.
6. **Preset Accordion:** Convert the filter preset list into an accordion component so clicking a preset expands its details inline, rather than navigating the user to a new view.
7. **V1 Filter Panel UI**: Make it similar to the updated filter panel UI
8. **Disable Form during preset edits:** Disable the edits in the filter form when "Save as preset" or "Save as existing preset" tray is opened.  
9. **Disable Filters Button instead of hiding** in query results page
10. **Setup Dev Page** for 3 cases. with react router sidebar filters, with portal sidebar filters, with both portal sidebar in react router to compare the complexity in each case.

## Filter Sidebar Requirements

### 1. Visibility & Layout
* **Trigger:** Opens if `filterSidebarOpen` OR `savedFilterSidebarOpen` is true.
* **Modes:** 
  * **Single-Mode (v1):** No tabs. Fallback if callbacks are missing.
  * **Dual-Mode:** Shows **Current** and **Saved** tabs (active when both callbacks exist).
* **Layout:** Tab headers sit on the right side of the title header.

### 2. "Current" Tab (Active Filters)
* **Actions:** Apply Filters, Clear, and **Save Filter**.
* **Save Form:** Requires **Title** and **Description**. 
  * *Option 1:* Temporarily replaces the main filter form.
  * *Option 2:* Displays in the panel footer (checkout-style).
* **Feedback:** Triggers success/error Toast via API response.

### 3. "Saved" Tab (Filter Presets)
* **Restriction:** Exclusively for the Filters-AST version.
* **Actions:** Fetch list (GET), Delete preset, and "Update Existing" (opens an overwrite dialog).
* **Inline Accordion:** Clicking a preset expands to show a compact preview with two options:
  * **Load:** Instantly applies filters and auto-switches to the **Current** tab.
  * **Edit:** Renders the form inline, changing the action button to **Save/Update** (uses a button loader during submission).

### 4. Core Capabilities
* **Tags:** Support tags filtering natively within Filters-v2.



## Tech Debt
- [ ] Remove the component: `FilterSidebarLayoutTemp` in favor of updated `FilterSidebarLayout` which uses `filterSidebarController` instead of individual `isFilterSidebarOpen` and `toggleFilterSidebar`. Also update all the usage of the `FilterSidebarLayout` component to use the `filterSidebarController` directly.
- [ ] Rename file: `table-filter-formV2.tsx` to `table-filter-form.tsx` and delete the file existing file `table-filter-form.tsx`
- [ ] Analyze the use of `src/components/data-table/dt-filter-form/select-filter-field.tsx` and if it should be deprecated/removed as well as the types/interfaces within it.
- [ ] Analyze the difference between `dt-server-side-search-field-v2.tsx` and `dt-server-side-search-field.tsx` and see if `dt-server-side-search-field-v2.tsx` is usable. If yes, then what is the change across the both versions. Maybe it was intended to accept the `filters` prop without casting `as IServerSideFilters | undefined`.
- [ ] Introduce the React Context for the Data Table components to avoid prop drilling, and use the compound component pattern for it.
- [ ] Why is FilterSidebar not the in same file as TableFilterForm. Why can't they be merged into one.


## Inspiration
![[Pasted image 20260614160856.png]]
![[Pasted image 20260614160905.png]]
![[Pasted image 20260614160916.png]]
![[Pasted image 20260614160920.png]]