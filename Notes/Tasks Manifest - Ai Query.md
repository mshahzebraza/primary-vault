---
organization: "[[aiquery.io]]"
categories:
  - "[[Work]]"
  - "[[aiquery.io]]"
  - "[[Tasks]]"
type: "[[Task]]"
status: active
projects:
  - "[[aq-client]]"
---

## ▶️ In Progress

- [ ] Fix the sql formatting in the query smith for linebreaks and indents
- [ ] allow the agent group renames using the admin api
- [ ] Use the recurring as the default selected mode in schedule dialogs
	- [ ] use ONE TIME instead of Non-Recurring everywhere for the schedule mode context
- [ ] Agent group selection from view to create query doesn't show up until we move through all the paginated response options
- [ ] Show the agent groups against resources
	- [ ] Show the agent  gropus belonging to the query (in detail page)
	- [ ] Show the agent  gropus belonging to the agents (in detail page; overview -> detail page)
	- [ ] Add Detail Pages to Query-Pack, Query-Schedule just like query and agent pages have their own detail/overview page (wednesday) - less priority
- [ ] Agent Groups Augmentation (using secondary fetch requests) and resolves the filter (Filter is harder)
- [ ] Tags filter selection list should be client-side searchable (combobox instead of regular selection)
- [ ] The AI Panel Initial Node is not auto selected when AI Panel is opened
- [ ] [[260624 Task - Sidebar v2 Redesign]]
- [ ] [[260612 UI Overhaul]]
- [ ] [[260611 Document ShadCN theming architecture setup and maintenance]]
- [ ] [[260624 Task - Ctrl+Enter Submit for SQL Editor with Hover Hint]]
- [ ] [[260518 Feat - Query Response Data Diffing | Query Response Data Diffing Tasks]]
- ➡️ [[260612 rapid response refactoring and enhancements]]
- ➡️ [[rapid-response bugs]]
- [ ] Update the TOTP Revert wording according to Nick's comment:
	> When shortened – just call it "2FA" or "MFA". When written out – "two factor authentication".
- [ ] `toast.promise` pattern causes toast for each failure instead of a single toast on final failure
- [ ] Add distinction of PPE vs PROD for Authenticator Name and browser channel API
- [ ] Fix overflow issue of query preview items (caused by scroll area overflow styles)
- [ ] Vertical scroll caused by too many exports in metadata tab of query detail view
- [ ] Revert the agent group custom extension test deployments
- [ ] Try to add Title+description JSX in select options of the change user role dialog
- [ ] Bug Bash Tasks ![[260417 April Bug Bash Meeting#Pending]]
- [ ] Refactor/Restructure the Login Form and MFA — prefer Compound Component Pattern
- [ ] Optimization: Team Settings & Role Management Tasks ![[260505 Task - Team Settings & Role Management#Optimization]]
- [ ] [[260406 add end to end testing of create query flow]]
- [ ] User is logged out even when active on another tab — sync session activity across tabs
- [ ] Create a variation pattern for the agent list views
- [ ] *Query Detail's Query List Panel* ![[260411 Create Query List Panel in Query Detail View#Pending]]
- [ ] Change highlighting of the sidebar from BLUE to PURPLE
- [ ] Rename dashboard collection/sections to dashboard tabs
- [ ] Current filters identification for all views
- [ ] **[[260406 update the shadcn version, components and theme]]**
- [ ] View Layout: handle help button dynamically; description and breadcrumbs should be optional
- [ ] use schema endpoint for filterable options in the response data table
- [ ] Optional: analyze if Compound Component Pattern for Data Table improves reusability
- [x] Show IP address in agent list by default — from [[260623 Weekly Scrum - UI Updates, Tags]]
- [ ] Liveshell layout redesign — from [[260623 Weekly Scrum - UI Updates, Tags]]
	- [ ] Liveshell panel should be to the right
	- [ ] History of recent commands in liveshell
	- [ ] Above: session duration + switch liveshell host (ends session before switching)
	- [ ] Below: device info (like agent info view block / rapid response hover card)
	- [ ] Right: AI assistance expanded; bottom aligned with bottom of left pane

### Refactoring
- Add Architecture and Patterns files for LLMs and devs (`skills.md`, `*.architecture.md` etc.)
- implement, refactor, standardize or sync:
	- url json state hook standardization
	- toast.promise
	- **NEW:** type-safe query-parameters handling API/usage simplification
	- filters-sidebar architecture documentation + HOC/protected-context pattern
	- [x] tabs content pattern
	- view-variants pattern
	- view-header/view-layout refactoring
	- custom extension code optimization
	- **NEW:** stepperize usage for wizards
	- standardize selection inputs and document when to use what selection inputs
	- upgrade to Tailwind and ShadCN latest
	- replace button component of ShadCN with new one and use theming

### Navigation
- ➡️ [[DashboardWidgets|Dashboard / Widgets]]
- ➡️ [[custom extension bugs|Custom Extension Bugs]]
- ➡️ [[Custom Extensions View (Bugs, Tasks and Optimizations)|Custom Extensions View]]
- ➡️ [[PPE to PROD checklist|PPE → PROD Checklist & Settings Tasks]]
- ➡️ 🔴 [[Filtering V2 - Athena, Clickhouse and MongoDB]]
- ➡️ 🔴 [[Possible Areas to Update of Filtering Architecture]]
- ➡️ [[260509 Task - Rapid Response View Enhancements]]
- ➡️ [[end to end prod testing & checklist|End-to-End Prod Testing Checklist]]

---

## 🟥 Pending

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

---

## ⚠️ Blocked

- ⏸️ 🟠 implementation of query diffs (blocked: after Filtering V2) — [[260518 Feat - Query Response Data Diffing]]
- ⏸️ 🟡 logs and metrics — [[Frontend - Observability (Logging & Metrics)|Frontend Observability]] (blocked: active tasks; may go to Rajput)
- ⏸️ 🟡 agent feature configuration (paused: needs more discussion)

---

## ✅ Completed

- [x] [[260509 Task - Rapid Response View Enhancements]]
- [x] [[260509 Task - Reset Password - Revert MFA Mode and Back to Login]]
- [x] [[260505 Task - MFA Feature (Firebase TOTP)]]
- [x] [[260609 Setup the Saved Searches]]

---

## Ideas/Future Requirements

- Tags on query packs and query presets — from [[260623 Weekly Scrum - UI Updates, Tags]] (tags on query entries already done; this extends to packs/presets)
- Hover tooltip on tag overflow badge (+N) — hovering the `+N` chip shows a card of hidden tags; very low priority (Nick follow-up)
- Fix field label mismatch: `created_at`/`created_by` displayed as "Initiated On"/"Initiated By" in query results — minor inconsistency (Nick follow-up)
- v2 API filters: add more filter types + filter panel support — from [[260623 Weekly Scrum - UI Updates, Tags]]
- Sub-Tenants — future (deferred in 2026-06-23 scrum)
- Ask Fleet MVP — flagged for future discussion

---

## Tech Debt

- [ ] Standardise the query param interface and schema logic
- [ ] Add code templates (`template.model.ts`, `template-view.hook.ts`, `template.hook.ts`, `template.api.ts`, `template.dto.ts`, `template.view.tsx`, `template.page.tsx`) with pseudo-code and instructions for: dialogs, tabs, toasts, one-off requests, and other edge cases
