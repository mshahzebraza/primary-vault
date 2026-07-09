---
type: "[[Journal]]"
categories:
  - "[[Personal]]"
date: 2026-07-09
tags:
  - journal
organization:
  - "[[aiquery.io]]"
related-tasks:
---
## Changes
- add some purple
- take out 
	- the total agents
	- analysis of AI
	- percentage/phase progress bar
- new session and history on top right
- don't need to be too enterprisey
	- remove the separation line

## Flow




New Sessions
- create session endpoint (Or Cancel Session V2)
- hit the endpoint `v2/ask-fleet`
	- payload
		- agent-groups
		- ask_prompt
	- backend: session created as pending/success - message aggregation is pending
	- client: user redirected to the session page. subscribe to streaming
- stream message endpoint (aggregate sql query + suggestions) (Cancel Message Response V2)
- stream message's query response result (first change: show, subsequent changes: notify)
- post aggregated-sql-search
- virtualized response

- new query message: dedicate create message in session endpoint


Session Comeback:
- get session info
- get all the previous messages in the session 
- All non-latest sessions response doesn't need to be shown (they would be closed to the user)
- stream the query repsonse result
- post aggregated sql search

History (History of Sessions)
- tab1: recents
	- section 1: recent session
	- section 2: recent questions
- tab 2: sessions
	- all sessions (not openable)

