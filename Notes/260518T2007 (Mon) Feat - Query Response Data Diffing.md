---
status:
  - active
tags:
  - task
  - architecture
organization: "[[aiquery.io]]"
categories:
  - "[[Work]]"
  - "[[Tasks]]"
type: "[[Task]]"
projects:
  - "[[aq-backend]]"
  - "[[aq-client]]"
  - "[[aq-devops]]"
priority: P1
---

## Status
Design document is complete — markdown lives in the docs repo, also shared as a Google Doc with the team.




## Tasks
## Completed
- [x] Design Document
- [x] Prototype implementation
### Pending
- Refresh the feature requirements/architecture/design documents
	- the views of the query detail diff
	- dfference b/w IO of prototype vs actual backend
- setup the step by step migration plan
		- setup the hello world function
		- setup the mongo connection and attempt retrieval of any single document
		- setup the retrieval of a specific query's response data and save in temp storage in the disk
		- accept the inputs of query ids and retrieve and store the response data of input query ids in the disk
		- migrate the algo to python
		- perform the algo on the received 2 sets of response data
- prototype code refactoring
		- separate the actual vs setup code
		- deprecate the stale code (which is not to be used in the production)
- [ ] Service Layer implementation (blocked: will be done when actually implemented)
