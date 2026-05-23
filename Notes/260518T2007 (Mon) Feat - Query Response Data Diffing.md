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
### Completed
- [x] Design Document
- [x] Prototype implementation
### Pending
- Refresh the feature requirements/architecture/design documents
	- the views of the query detail diff
	- dfference b/w IO of prototype vs actual backend
	- run the prototype
- setup the backend-infra trigger
	- add endpoints for validation and initiation of query-diffs
	- don't accept the query executions if there's no common agents or if the common agents have not responded with any data to diff
	- resolve the agent groups to valid agents (avoid calling mongodb from the serverlesss)
	- batch the list of resolved common agents if exceeding the max agent list (compute the payload size supported by 1mb size cap)
	- save a pending query-diff document and initiate a work message in the query-diff queue
	- mount the work messages into a new query diff job queue (batch them if required)
	- listen for the processed batches from the serverless after the computing of the query-diff (or its batches is done) and accordingly update the query diff pending document
- setup the step by step migration plan
		- setup the hello world function
		- retrieve the query-response data from clickhouse for the 2 executions for each of common agents and process the diffing.
		- assume that the sorting of the `data` field for query-response-data document is not required since, clickhouse ensures that the data is stored and retrieved always in the same way, so the stringification of the data results in a deterministic key always
		- keep storing the diff results locally (in disk) until the entire batch is processed
		- When processing is done
			- save the diffing result in the s3 bucket (this will queries using s3-athena by the backend-infra repo code)
			- **send out the message in the queue to the serverless with an appropriate type**
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

### Discussion with Rajput

quesitons

if one agent execution is a too long list 
should I even fetch per agent

the resolved agents are too many to show to the users

empty data should be considered for diffing
any pointers on validating the code
parquet


4-6000 rows roughly equals 1mb from agent 
at max 1mb or smaller than 1000 agents. Clickhouse recommends keeping the IN statement for querying data within a list of 1000 items

- **save the resolved exeuction targets in the db against the diff with a ttl, and also enrich these agent documents.**
query diff document should be created with the validation endpont, with the state of 'validation'.
OPitonal Optimization: Batch the list of resolved agents to insert in the mongodb instead of inserting 6000 agents in the mongodb at once.
need a dedicated data table
- how to convert json to parquet
- check if the ordered document when sconverted to entries, always result 

- figma for query diff
- fix the query composer responsiveness
- agent ids should be copy-able from the UI directly 