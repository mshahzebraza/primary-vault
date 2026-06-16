---
type: "[[Meeting]]"
categories:
  - "[[Personal]]"
  - "[[Meetings]]"
date: 2026-06-16
tags:
  - journal
organization:
  - "[[aiquery.io]]"
projects:
  - "[[aq-backend]]"
  - "[[aq-client]]"
attendees:
  - "[[Nick]]"
  - "[[Rajput]]"
  - "[[Zahi]]"
status:
  - active
related-tasks:
  - "[[260609T2043 (Tue) Setup the Saved Searches]]"
---

## Context
> Brief note on why this meeting happened / what triggered it.

## Discussion
- Investigation UX
- Analyze Flow
- Testing
- Ask the Fleet
	- prompt the fleet about the queries in human language
	- would run the query and aggregate the search on the query response
- File Detonation (way later)
	- to investigate an exe file by detonating it.
	- detonating it in a sandbox, and returns the monitoring data
- aiquery becoming the IR and Compliance tool now
	- for companies that don't have a dedicated IR tool; and are not that big
	- Gap between EDR/Monitoring Tools etc.
 
## Unknowns
- EDRs - how they relate to conclusive analysis (EDR)
- NDR/XDR? (Network, Extended)
- `dll` files in temp directory

- how you catch it when it happens for large corps for the things that its collecting
	- they don't. They just assume the bugs and they take action (mostly manually)
- what do you do when you find an issue in realtime
	- AV might block it on their own
		- v1: changing hash
		- v2: P headers - based on sequence of executions or binary bits
		- v3: EDR Telemetry - comparison with hashes - behaviors lookups
			- if unknown binary runs this file => block
			- divergence of patterns - behavior
	- they could ask the fleet manager to do operations to stop network comm altogether
	- OR they could refine on the investigation
		- they could single out and monitor
		- and they could also try to figure out why the machine/malware got in
		- Or they could wipe it out
	- So basically **containment & identification** is the main response. (or "should-be" response)
	- then they liveshell into their devices from their dedicated tools.
	- but they always do it on their own mostly instead of tools.
	- *Is their a bulk write tools*
- we might also be about WHEN it happens (instead of before and after only)
	- *using MCP and alerts*
	- can a pair of mcp client and server be communicating to each other?
	- *do we need to ask for admin permission to trigger investigation. since they are not available.*
## Action Items
- [ ] Ask Rajput for the UX flows and ask for understanding