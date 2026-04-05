---
organization: '[[aiquery.io]]'
categories:
- '[[Work]]'
- '[[aiquery.io]]'
- '[[Tasks]]'
type: '[[Documentation]]'
status: active
---
## Legend
⏸️: Pending Status
➡️: Active Status
⏩: Delegated
🟡: P0 (Highest) Priority
🟠: P1 (Medium) Priority
🔴: P2 (Low) Priority

## Active Tasks

- ➡️ [[DashboardWidgets|Dashboard / Widgets]]
- ➡️ [[custom extension bugs|Custom Extension Bugs]]
- ➡️ [[Custom Extensions View (Bugs, Tasks and Optimizations)|Custom Extensions View]]
- ➡️ [[PPE to PROD checklist|PPE → PROD Checklist & Settings Tasks]]
- ➡️ [[Marketing Website]]
- ➡️ [[aiquery exports task|Exports]]
- ➡️ 🔴 [[Filtering V2 - Athena, Clickhouse and MongoDB]]
- ➡️ 🔴 [[Possible Areas to Update of Filtering Architecture]]
- ➡️ Rapid Response
	- [[rapid response refactoring and enhancements]]
	- [[rapid-response bugs]]
- ➡️ [[end to end prod testing & checklist|End-to-End Prod Testing Checklist]]
- 🔴 number of results in devices tab (+ execution time etc)
- 🔴 add response/device in infra api (agent not connected)
- [ ] use the target-device refactoring branch to merge into develop
- [ ] update the shadcn version
- [ ] add end to end testing of create query flow
- [ ] rename the dashboard collection/sections to dashboard tabs
- [ ] ensure that the timepicker form field is reusable; not specific to dashboard widgets

## Blocked Tasks
- ⏸️ 🟠 implementation of query diffs (blocked: after filtering v2) — [[Query Response Data Diffing]]
- ⏸️ 🟡 inactivity timeout for console (blocked: filtering v2)
- ⏸️ 🟡 logs and metrics — [[Frontend - Observability (Logging & Metrics)|Frontend Observability]] (blocked: active tasks; may go to Rajput)
- ⏸️ 🟡 agent feature configuration (paused: needs more discussion)

## Todo Tasks

### High Priority
- 🔴 [[BUG - Race condition on custom extension Test & Publish tab]]
- 🔴 Change verbiage of assessment results navigation tab

### Medium Priority
- 🟠 [[Task - Add Debouncing to Table Search Input|Add Debouncing to Table Search Input]]
- 🟠 the query preset title shouldn't be cut off
- 🟠 compare public APIs vs private APIs logic parity

### Low Priority
- 🟡 [[Feature Planning - Date Filters|Date filters for date fields]]
- 🟡 migrate from `nodemailer` to `aws ses` — see [[Implementing AWS SES in Nest JS Application]]
- 🟡 pagination in public APIs — may be using old implementation
- 🟡 class-based typed API call builder
- 🟡 BUG: active column filters dropdown keeps closing
- 🟡 BUG: teams and invites view dropdowns close on first click

## Completed
- ✅ [[Fix devices MultiSelect|Fix: Devices MultiSelect pagination bug]] — PR #380 merged
