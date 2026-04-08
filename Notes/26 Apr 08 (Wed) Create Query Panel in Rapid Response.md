---
type: "[[Task]]"
categories:
  - "[[Work]]"
date: 2026-04-08
tags:
  - feature
organization:
  - "[[aiquery.io]]"
projects: []
status:
  - active
priority: P2
---

## Overview
> It is inconvenient to compare each instance of a query pack query by view detail of each query-run separately. We need a way to quickly toggle between the different variations of the query-pack

[UI Link](https://www.figma.com/design/JoOPDwbtWdrqaz1XliNG97/AI-Query?node-id=6739-42719&t=8nwlskO6nhDPGkY8-4)
## Current Tasks
## 2026-04-08
- [ ] Create a [[#Plan|plan for the implementation]]
- [ ] Create a query-panel
- [ ] How to keep the filters intact for the query detail.
	- The query click is supposed to change the query-param in the url, which *might* always trigger the new page mount, causing the state to be lost for the view. *Please confirm this...*
	- If this unmount is inevitable, should we keep the filters in the local storage somewhere?

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


![[Related Meetings.base]]

