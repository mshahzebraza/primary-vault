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
	- [ ] filters v2 should replace filters v1 for query detail view
	- [ ] rapid response is always enabled
	- [ ] query-charts is scraped off completely.
- [ ] backend will look into the issue of the `[eq]` filter for the query detail's devices tab as other endpoints are correctly handling the eq filter

![[Related Tasks.base]]

