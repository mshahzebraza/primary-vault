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
	- run the prototype
- setup the step by step migration plan
		- setup the hello world function
		- setup the mongo connection and attempt retrieval of any single document
		- setup the retrieval of a specific query's response data and save in temp storage in the disk
		- accept the inputs of query ids and retrieve and store the response data of input query ids in the disk
		- migrate the algo to python
		- perform the algo on the received 2 sets of response data
		- save it in db
- prototype code refactoring
		- separate the actual vs setup code
		- deprecate the stale code (which is not to be used in the production)

## Queries
- Db to use to store the data? Clickhouse or MongoDB
- Do we need to add the export support?
- Do we need to add filtering support
- how to validate and match devices name for baseline and target query.
- agent groups need to resovle for both baseline and target execution
	- use `{groups: {$in: [...agent-group-targets]}}`

## Discussions
- Validate if queries match (regardless of order)

- send a message to sqs service for serverless functions
```
// copy the pattern of query response data action result, processing type
// there's some standard files
{
	type: 
	tenant_id, 
	baseline_id, 
	target_id, 
	diff_targets: { all: boolean OR agent-ids: [] } }
```

- lambda always assumes its given the truth. and it attempts to find the data in the clickhouse. If no data is available, it would say no match, or fail

- return as much data as we might need in future to avoid migrations. like `execution_type`: `on-demand`/`policy-run`


- Note: Make sure the queries are completed agianst which you're creating the diff in the client