---
organization: "[[aiquery.io]]"
categories:
  - "[[Work]]"
  - "[[aiquery.io]]"
  - "[[Tasks]]"
type: "[[Documentation]]"
status: active
---
## Active Tasks


-  Make the header of views compact
	- The header should have Panel Close Button, followed by the Title (Or Breadcrumbs if nested route).
	- The description would be kept in the view-title-hover-card.
	- The right of the header row, would house the Docs Button for the view.
- [ ] [[260609T2043 (Tue) Setup the Saved Filters for Query List]]
- [ ] Optional:  Analyze if its a good thing to allow Compound Component Pattern for the Data Table instead of a single component receiving props for better reusability
- [ ]  use the schema endpont for showing the exact filterable options i.e. for the response data table. For others we'll keep relying on the table data's rows. (or we could technically create a single row call to be used as schema endpont fallback and cache it for the view rendering)


- [x] Agent and Agent Group Overview Summary
	- *Optional* - Create a centralized and reusable service summary schema, and reuse it for agent and agent groups
- [x] Change Auto to windows in query mode. And remove auto
- [x] Reasoning effort ai generator
- [[260518T2007 (Mon) Feat - Query Response Data Diffing | Query Response Data Diffing Tasks]] 


- Refactoring
	- Add Architeture and Patterns  Files for LLMs and Devs (i.e `skills.md`, `*.architecture.md` etc.) with a dedicated compact section of rules/guides/implementation-notes as well as description/explanation for detailed understanding
	- implement, refactor, standardize or sync the following:
		- url json state hook standardization
		- toast.promise
		- **NEW:** type-safe query-parameters handling api/usage simplication
		- filters-sidebar architecture documentation + hoc/protected-context pattern
		- [x] tabs content pattern
		- view-variants pattern
		- view-header/view-layout refactoring
		- custom extension code optimization
		- **NEW:** stepperize usage for wizards
		- standardize selection inputs and document when to use what selection inputs
		- upgrade to tailwind and shadcn latest
		- replace button component of shadcn with new one and use theming
- [ ] View Layout
	- should handle the help button dynamically (most probably in the row of the title with top right corer block)
	- description and breadcrumbs design should be optional
- [ ] Update the TOTP Revert wording according to Nick's comment.
>	Ok so a few things:
>	I cannot load that video for some reason? :lolsob: 
	Yeah I agree that the wording of calling it "second factor" is kinda weird and not how anyone talks lol
	Here is how I would change it:
	When shortened – just call it "2FA" or "MFA"... thats industry standard and everyone knows what that means
	When written out – just call "two factor authentication"...that is also valid and industry standard (plus we only allow ONE additional auth mechinism, so saying its a second factor implies maybe there is a third, vs just saying two-factor)
- [ ] `toast.promise` pattern causes toast for each of the failure, instead of showing a single toast on final failure
- [ ] Add a event listener to submit active query on Pressing `Ctrl + Enter` in the sql editor, specifically on the rapid response editor. Also show a hovering card, presenting the hint.
	- Prompt: Also, is it possible to change the SQL editor component in a way that it allows a callback to be used for the control enter key press? I'm asking this because when on an input field, we press enter, it automatically submits the form. However, for the SQL editor, we have to use the mouse, even when we are in the editor and we have typed our entry. We can't just control enter and expect it to work as a submit call. We necessarily have to use a mouse currently. So, is there a solution to that where we show a hovering hint to the user, absolutely positioned on the bottom right of the SQL editor, and only visible with subtle styles when it is detected that the user has stopped typing for, let's say, a second? So it's only when the user has stopped typing for a second that we show the hint. But the functionality to control enter should always be listening so that a user who already knows how the control enter functionality works can use it without waiting on the hint. But for new users, the hint would help them. If the system detects inactivity for the SQL editor, they can prompt the user to click control enter to submit the text, or something. And, of course, this hint should only be visible if the callback is passed, and this hint should also be configurable with a default value which is generic and short.  
- [ ] Add distinction of PPE vs PROD for Authenticator Name as well as browser channel api
- [ ] Fix the Overflow issue of the query preview items caused probably by scroll area overflow styles
- [ ] Reset Password - Revert MFA Mode and Back to Login ![[260509T2233 (Sat) Task - Reset Password - Revert MFA Mode and Back to Login#Current Tasks]]
- [x] Enable Copy to Clipboard of RO_TextField should be bigger and only visible on hover
- [ ] Vertical Scroll Caused by too manu exports in metadata tab of query detail view
- [ ] Revert the agent group custom extension test deployments
- [ ] Try to add Title+descript JSX in select options of the  change user role dialog
- [ ] Bug Bash Tasks ![[260417T2004 (Fri) April Bug Bash Meeting#Pending]]
- [ ] Refactoring
	- [ ] Refactor/Retructure the Login Form and MFA to preferably use the Compound Component Pattern
- [x] The disabled MFA is not updated in the team settings table
- [ ] Optimization: Team Settings & Role Management Tasks ![[260505 (Tue) Task - Team Settings & Role Management#Optimization]]


- [ ] [[260406 (Mon) add end to end testing of create query flow]]
- [ ] User is logged out even when he is active on another tab. Need to sync the session activity across browser tabs.
- [ ] Create a variation pattern for the agent list views
- [x] MFA Feature Screen [[260505 (Tue) Task - MFA Feature (Firebase TOTP)#Tasks]]

- [ ] *Query Detail's Query List Panel - Pending Tasks*![[260411 (Sat) Create Query List Panel in Query Detail View#Pending]]
- [ ] Change highlighting of the sidebar from BLUE to PURPLE
- [ ] rename the dashboard collection/sections to dashboard tabs
- [ ] current filters identification for all views
- [ ] **[[260406 (Mon) update the shadcn version, components and theme]]**
- Rapid Response View Enhancements![[260509T1213 (Sat) Task - Rapid Response View Enhancements#Current Tasks]]




- ➡️ [[DashboardWidgets|Dashboard / Widgets]]
- ➡️ [[custom extension bugs|Custom Extension Bugs]]
- ➡️ [[Custom Extensions View (Bugs, Tasks and Optimizations)|Custom Extensions View]]
- ➡️ [[PPE to PROD checklist|PPE → PROD Checklist & Settings Tasks]]
- ➡️ 🔴 [[Filtering V2 - Athena, Clickhouse and MongoDB]]
- ➡️ 🔴 [[Possible Areas to Update of Filtering Architecture]]
- ➡️ [[260509T1213 (Sat) Task - Rapid Response View Enhancements]]
	- [ ] Add **Actions** dropdown (load preset / save as preset / go to create query)
	- [ ] Add "Save as preset" action to individual query history items
	- [ ] *(Optional)* Multi-select on history items to batch-save as a preset
	- ➡️ [[rapid response refactoring and enhancements]]
	- ➡️ [[rapid-response bugs]]
- ➡️ [[end to end prod testing & checklist|End-to-End Prod Testing Checklist]]
## Blocked Tasks
- ⏸️ 🟠 implementation of query diffs (blocked: after filtering v2) — [[260518T2007 (Mon) Feat - Query Response Data Diffing]]
- ⏸️ 🟡 logs and metrics — [[Frontend - Observability (Logging & Metrics)|Frontend Observability]] (blocked: active tasks; may go to Rajput)
- ⏸️ 🟡 agent feature configuration (paused: needs more discussion)

## Backlog Tasks

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
### Refactoring / Tech Debt
- [ ] Standardise the query param interface and schema logic
- [ ] Add code templates (`template.model.ts`, `template-view.hook.ts`, `template.hook.ts`, `template.api.ts`, `template.dto.ts`, `template.view.tsx`, `template.page.tsx`) with pseudo-code and instructions for: dialogs, tabs, toasts, one-off requests, and other edge cases
