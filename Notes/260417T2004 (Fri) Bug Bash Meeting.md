---
type: "[[Meeting]]"
categories:
  - "[[Personal]]"
  - "[[Meetings]]"
date: 2026-04-17
tags:
  - bug
  - task
  - minor-tasks
organization:
  - "[[aiquery.io]]"
projects:
  - "[[aq-client]]"
  - "[[aq-backend]]"
attendees:
  - "[[Rajput]]"
  - "[[Nick]]"
---

## Context
> We need to find and mark bugs for removal later. 

## Discussion

## Decisions Made

## Action Items
- [ ] Remove the Mitre Link in Yara Mode
- [ ] Update Link in Windows Event Log Mode (Or add it as a Second Link: *Windows Event Catalog*. Rename the existing one as *Window Security Events*)
- [ ] Need to update the yara mode text blurb
- [ ] Rapid Response History Item
	- [ ] Save the rapid response history data as well
	- [ ] Save the name of Device in the history context
	- [ ] Point rapid response 'Need Help?' link to rapid response page



### Bugs
- [ ] Optional: timezone selection should preferable use local TZ selection
- [ ] Daylight Saving Timezone Issue (Need to Swap automatically; Look for better solution)
		- [ ] Second Sunday march moves forwards New York is -4
		- [ ] First Sunday in november go back to New York is -5
- [ ] Keep the logout on inactivity consider the activity on other tabs before logging user our

#### Team Page
- Refresh on team view doesn't show toast
- search doesn't work on team page
	- dual filters on team table page, i.e. `filters[user.name][regex]` and `user.name[regex]` filters
- role text for system roles should not include `(Default)` 
- 
