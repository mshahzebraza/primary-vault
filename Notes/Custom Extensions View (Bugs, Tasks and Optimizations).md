---
status: active
tags:
  - feature
organization: "[[aiquery.io]]"
categories:
  - "[[Work]]"
  - "[[Tasks]]"
type: "[[Task]]"
projects:
  - "[[aq-client]]"
priority: P2
---

## Overview
Custom Extension creation and management view — multi-step form (metadata → code → testing → publish).

## Current Tasks

### In Progress
- 🔴 Let the code type be supported, or hide the code option for now
- 🟡 Add build button in code tab + show details of previous build
	- Build should be compulsory in the code step; remove build from the testing tab
- Add resizing functionality to the data-table
- MSP Figma touchup + cleanup Figma
- Check how deployment section checks staleness; design a better centralised status state management approach
- [ ] (open)

### Pending
- P1: Bug — metadata not populating in latest refactoring branch commit
- P2: When new build is added, why can't we redeploy without undeploy first?
- P2: UI — Add a banner error when code prerequisite fields change
- P3: Review working of form submit handlers in the metadata form
- P4: BUG — `dirty` is out of sync with `dirtyFields` again
- Build Complete → Rebuild flow broken
- Deploy Pill: changes to "loading" then reverts to "Not Started"
- Remove code label from editor form input in code tab

### Architecture / R&D Questions
- P3: Why can't we fetch the table schema in the table schema dialog directly instead of relying on `getPreviewData` from the store? How does the table-schema dialog work in the custom extension detail view when opened from publish?
- PX: Refactor the wrapper and custom extension data-fetching logic based on the id in the store — as a hook that fetches and updates specific store fields
- PX: If metadata steps are not updated, how will the staleness logic work in subsequent steps?
- PX: Create a hook/provider/context for fetching custom extension form data based on the id (similar to current pattern)

## Completed
- ✅ Remove schema sample limit restriction
- ✅ Truncate uploaded schema sample to last 100 lines in logs
- ✅ Show next + generate button
- ✅ Show code view in extension detail view
- ✅ Fix: ai-gen-code not auto-added to custom extension POST/PUT call
- ✅ BUG: `dirtyFields` not in sync with `isDirty` in code form
- ✅ Remove mapping functions — map responses and form values to each other directly
- ✅ Investigate store usage for form values — simplified to id-only from store, rest fetched via API
- Note: `get-custom-extension-by-id` endpoint doesn't return code/content — should be removed from DTO response

## Related Meetings
