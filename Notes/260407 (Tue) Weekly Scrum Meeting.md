---
type: "[[Meeting]]"
categories:
  - "[[Work]]"
  - "[[Meetings]]"
date: 2026-04-07
tags:
  - journal
  - scrum
organization:
  - "[[aiquery.io]]"
projects:
  - "[[aq-client]]"
attendees:
  - "[[Rajput]]"
  - "[[Nick]]"
---
## Context
> Brief note on why this meeting happened / what triggered it.
## Discussion
## 2026-04-07
- Discuss the tasks in [[260406 (Monday) - Developers Meeting]]
	- add the disclaimer for filters applied
	- [[Rajput]] showed draft ui for investigations 
	- query-list panels in the rapid response and query detail
	- BUG: query editor gives UI jerk when content in the editor is too much due to a resizing change added earlier. Steps to repro;  
		- Add a realistic query - you can just do select * from users, or load a preset
		- Then open save preset or schedule, the SQL editor in the pop up module should be incorrectly sized - then if you add anything at that point (space, character, etc.) you will see it snap back to the right size
	- [[260409 (Thu) BUG - Data Table pagination row causes the parent container to scroll|BUG: Data Table pagination row causes the parent container to scroll]]

## Decisions Made

## Action Items
- [x] BUG: the color of Mac Icon is not respecting the black color override in the query-smith query composer (See [Nick's Message](https://aiquerytesting.slack.com/archives/C07LN92GW94/p1775660288811639))
	- Was fixed by making every os icon always be colored