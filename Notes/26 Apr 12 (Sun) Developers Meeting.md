---
type: "[[Meeting]]"
categories:
  - "[[Meetings]]"
  - "[[Work]]"
date: 2026-04-12
tags:
  - scrum
organization:
  - "[[aiquery.io]]"
projects:
  - "[[aq-client]]"
attendees:
  - "[[Rajput]]"
---

## Context
> Updates on integration of the query-list panel and 

## Discussion
- updates on the query-list panel of the query detail view
	- decision to move away from local storage
	- informed little refactoring and optimization is pending
- disccussed the removal of deprecated and stable feature flags
## Decisions Made/Action Items
- [ ] filters identification in the query list panel of the query detail view
	- [ ] current filters identification
	- [ ] query list panel's active filters cache identification
- [ ] removal of feature flags
	- [x] filters v2 should replace filters v1 for query detail view
	- [x] rapid response is always enabled
	- [x] query-charts is scraped off completely.
- [ ] backend will look into the issue of the `[eq]` filter for the query detail's devices tab as other endpoints are correctly handling the eq filter

## Further Feedback from Nick
### Feature Flags (FF) Cleanup
- [x] Enable `Rapid Response` by default.
- [x] Remove the `general v2` feature flag (or move it to 'internal').
- [x] Enable `Compliance` by default. 
- [x] Move the `Dashboard` feature flag to 'internal' for the time being.

### Compliance Mode Updates
- [x] Rename all UI text from 'Compliance' to 'Vulnerability' (Exception: Keep it as 'Compliance' inside the Marketing FF).
- ~~Remove the empty/non-filled-in tabs within this mode.~~
- [x] Ensure the internal Marketing FF remains intact and untouched.

### Cosmetic Changes
- [x] move export buttons to default behavior
- [ ] change vulnerability text and api call