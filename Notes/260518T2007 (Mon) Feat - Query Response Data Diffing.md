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
- setup the infra trigger
	- add endpoints for validation and initiation of query-diffs
	- save a pending query-diff document and initiate a work message in the query-diff queue
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

- 2nd validaton on actual trigger should also run. prefer caching in memory
- query export queue - sending export messages to serverless
- post query response data action results queue - should used for query diff results 
- query diff - to serverless


- infra would track the batches resolution and show a success progress based on the resolved batch messages from serverless

- parquet file system to be used ??? 
	- compressess the data alot
	- we need a new athena based AST - need an adapter to athena SQL
	- setup athena

- Note: Make sure the queries are completed agianst which you're creating the diff in the client

- `query-diff/validate`
```
// is there any common execution targets for the 2 runs
// cache the resolved common list of agents
// OPTIONAL: return the execution targets on which the diff can run (exclude the ones which wasn't common between the 2 executions or against which no data was received in either of these 2 executions)

POST /query-diff/validate
{
	baseline_query_id,
	target_query_id
}

```
- `query-diff/create`
```
// is there any common execution targets


POST /query-diff/create
{
	baseline_query_id,
	target_query_id,
	execution_targets: 'all-valid-execution-targets' | [target-a, target-b, ...]
}


// Atleast one or more agents or agent-groups selected as execution targets don't return invalid/empty data, and therefore a diff was not generated for them. The diff operation is in progress for remaining execution_targets
```

query diff prompt: (till conceptual sql)
```
What does "Prefer requiring compatible SQL/question context for apples-to-apples comparison." in the backend validation mean?

Does this mean that we backend is supposed to ensure that the sql of baseline and target query is semantically same even if not exactly same i.e. SELECT A, B FROM X should be seen as semantically equal to SELECT B,A FROM X. even when the sql string is not the same.

If this is what it means than mark it as optional and v2 enhancement and implementation should mark it with jsdocs. Otherwise add this as well in the validation section and explain the former question.

  

Also, the inline documentation for caution against failed, warning agents shoud be added in the actual implementation with a possible enhancement/update to filter out the warning agents. For now we go with the recommended approach of includint the success and warning rows if exist.

  

Furthermore, should the resolution of agent groups to agents also happen at the backend level and passed to the serverless as a plain agent list so that the serverless function doesn't have to resolve it into agents.

The downside is that the message might then contain possible a list of thousands of resolved agents which might exceed the message payload size allowed for sqs resulting in a failed pipeline. I'm inclined towards letting the serverless connect to mongodb to resolve the agent groups into the agents list. but then if the exclusion list is vrey large then it should still be supported by the sqs payload size, though its going to be smaller than the original execution targets. Please confirm the max size of the message for sqs which the serverless would read, I did a quick search saying its 1mb but not sure. Please confirm.

  

Furthermore, type on result queue matters much more than on work queue. and that should be documented somewhere in the plan.

  

Also can you please explain the conceptual sql? I'm getting the impression that you're fetching all the rows against both runs in one go instead of fetching per agent sequentially and processing it along with agent batch. Please tell what approach are you going with and how.
```