---
type: "[[Meeting]]"
categories:
  - "[[Personal]]"
  - "[[Meetings]]"
date:
  "{ date: YYYY-MM-DD }":
tags:
  - journal
organization:
  - "[[aiquery.io]]"
projects:
  - "[[aq-client]]"
attendees:
  - "[[Nick]]"
  - "[[Rajput]]"
status:
  - active
---
## Discussion
- tags should be applied to query packs, query presets
- add other filters in the v2 apis and support for them in the filters panel
- Liveshell
	- history of recent commands
	- above: 
		- how long session is going on
		- switch liveshell host (which when clicked should end the session before switching host)
	- below: device info (like the agent info view block; or the rapid response hover card)
	- right: ai assistance expanded; bottom should be aligned with the bottom of the left pane (terminal + card-at-bottom)
- *add the search for the views* -> NO. for now 
- Sidebar v2
	- icons removal of nested views
	- Initial Avatar with initials like google meet
	- Show Tenants as items when clicked on current tenant block
	- Show `user-role` alongside tenant name
	- the top block is for the SWITCHING (tenant name, user role)
	- the bottom block is for the USER (name and email) and LOGOUT
- *Sub-Tenants* - Future
- *Brand  color standardization*: Purple Shade
- *color of the sidebar* - should be brand color
- *Ask Fleet MVP Discussion*
## Decisions Made

## Action Items
- [x] `exist[query_sandbox] = false` (Urgent)
- [x] add tags to the query entries columns
- [ ] info message showing filters are applied in the view
- [ ] liveshell panel should be to right
- [ ] settings UI has content touching the header. add spacing
- [ ] liveshell - ai assistance input needs to expand to atleast 2 lines (like the generate ai input. and scroll vertically instead of horizontal)
- [ ] show the IP address in the agent list by default
- [ ] Figma for Sidebar
