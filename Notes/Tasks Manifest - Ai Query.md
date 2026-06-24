---
organization: "[[aiquery.io]]"
categories:
  - "[[Work]]"
  - "[[aiquery.io]]"
  - "[[Tasks]]"
type: "[[Task]]"
status: active
---

## ▶️ In Progress

- [ ] [[260612T2031 (Fri) UI Overhaul]]
- [ ] [[260611T2153 (Thu) Document ShadCN theming architecture setup and maintenance]]
- [ ] [[260624T2222 (Wed) Task - Ctrl+Enter Submit for SQL Editor with Hover Hint]]
- [ ] [[260518T2007 (Mon) Feat - Query Response Data Diffing | Query Response Data Diffing Tasks]]
- [ ] Reset Password - Revert MFA Mode and Back to Login ![[260509T2233 (Sat) Task - Reset Password - Revert MFA Mode and Back to Login#Current Tasks]]
- [ ] Rapid Response View Enhancements ![[260509T1213 (Sat) Task - Rapid Response View Enhancements#Current Tasks]]
	- [ ] Add **Actions** dropdown (load preset / save as preset / go to create query)
	- [ ] Add "Save as preset" action to individual query history items
	- [ ] *(Optional)* Multi-select on history items to batch-save as a preset
	- ➡️ [[260612T2035 (Fri) rapid response refactoring and enhancements]]
	- ➡️ [[rapid-response bugs]]
- [ ] Update the TOTP Revert wording according to Nick's comment:
	> When shortened – just call it "2FA" or "MFA". When written out – "two factor authentication".
- [ ] `toast.promise` pattern causes toast for each failure instead of a single toast on final failure
- [ ] Add distinction of PPE vs PROD for Authenticator Name and browser channel API
- [ ] Fix overflow issue of query preview items (caused by scroll area overflow styles)
- [ ] Vertical scroll caused by too many exports in metadata tab of query detail view
- [ ] Revert the agent group custom extension test deployments
- [ ] Try to add Title+description JSX in select options of the change user role dialog
- [ ] Bug Bash Tasks ![[260417T2004 (Fri) April Bug Bash Meeting#Pending]]
- [ ] Refactor/Restructure the Login Form and MFA — prefer Compound Component Pattern
- [ ] Optimization: Team Settings & Role Management Tasks ![[260505 (Tue) Task - Team Settings & Role Management#Optimization]]
- [ ] [[260406 (Mon) add end to end testing of create query flow]]
- [ ] User is logged out even when active on another tab — sync session activity across tabs
- [ ] Create a variation pattern for the agent list views
- [ ] *Query Detail's Query List Panel* ![[260411 (Sat) Create Query List Panel in Query Detail View#Pending]]
- [ ] Change highlighting of the sidebar from BLUE to PURPLE
- [ ] Rename dashboard collection/sections to dashboard tabs
- [ ] Current filters identification for all views
- [ ] **[[260406 (Mon) update the shadcn version, components and theme]]**
- [ ] View Layout: handle help button dynamically; description and breadcrumbs should be optional
- [ ] use schema endpoint for filterable options in the response data table
- [ ] Optional: analyze if Compound Component Pattern for Data Table improves reusability

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
- ➡️ [[260509T1213 (Sat) Task - Rapid Response View Enhancements]]
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

- ⏸️ 🟠 implementation of query diffs (blocked: after Filtering V2) — [[260518T2007 (Mon) Feat - Query Response Data Diffing]]
- ⏸️ 🟡 logs and metrics — [[Frontend - Observability (Logging & Metrics)|Frontend Observability]] (blocked: active tasks; may go to Rajput)
- ⏸️ 🟡 agent feature configuration (paused: needs more discussion)

---

## ✅ Completed

- [x] [[260609T2043 (Tue) Setup the Saved Searches]]
- [x] Agent and Agent Group Overview Summary
	- *Optional* — Create a centralized and reusable service summary schema, and reuse it for agent and agent groups
- [x] Change Auto to windows in query mode. Remove auto
- [x] Reasoning effort AI generator
- [x] Enable Copy to Clipboard of RO_TextField — bigger, only visible on hover
- [x] The disabled MFA is not updated in the team settings table
- [x] MFA Feature Screen [[260505 (Tue) Task - MFA Feature (Firebase TOTP)#Tasks]]

---

## Ideas/Future Requirements

---

## Tech Debt

- [ ] Standardise the query param interface and schema logic
- [ ] Add code templates (`template.model.ts`, `template-view.hook.ts`, `template.hook.ts`, `template.api.ts`, `template.dto.ts`, `template.view.tsx`, `template.page.tsx`) with pseudo-code and instructions for: dialogs, tabs, toasts, one-off requests, and other edge cases
