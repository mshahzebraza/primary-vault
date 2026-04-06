---
organization: "[[scholarbee]]"
categories:
  - "[[Work]]"
  - "[[Tasks]]"
type:
  - "[[Task]]"
status: active
tags:
  - orphan-tasks
  - minor-tasks
  - evergreen
projects:
  - "[[sb-backend]]"
  - "[[sb-ops-scripts]]"
---

## Document Intent
This document is meant to document the tasks that do not warrant a dedicated document-note yet. These are the notes which are crude or minor

## ▶️ In Progress
- [[26-Apr-06 (Mon) Bug - Program Search listing ranking issue in Student Portal]]

## 🟥 Pending
- [ ] Search Listing to conform to the requirements criteria submitted by the [[SB Outreach Team]]
- [ ] Favourite program notification
- [ ] Review the program creation flow outside the admin CMS (from university portal)
- [ ] University dropdown lookup should search against both abbreviation and name
- [ ] Add Draft Admission Program functionality
	- Add ability to create draft admission programs; hide in ES indexing and DB results
- [ ] R&D on Elastic Search storage options
- [ ] Data Inconsistency due to missing fields
	- Data Team should be informed about the es-indexing failures due to bad/stale data

## ⚠️ Blocked
- Commit the program template data from data entry into the database
- Review Shahwaiz Chat Socket Testing Video
	- Blocked; pending on Shahwaiz
- Timezone Filtering
	- Blocked; needs discussion
	- If frontend handles timezone conversion, backend date-only APIs will be offset; need decision
## 🟥 Unresolved — Program Creation from University Portal
Architecture decisions still needed:

- Should university admins be allowed to **create** program templates directly, or only **request** creation (requiring super-admin approval)?
  - If allowed: a lookup API must be provided matching against `abbreviation`, `name`, and `field_of_study`

- If direct creation is allowed, how do we prevent race conditions creating duplicate templates with the same name?
  - Option: make `(name + degree_level)` a unique compound key in the schema

- Should we allow university admins to use existing program endpoints and **auto-create** a program template if none exists with the same title?
  - Problem: if a template with the same name but different `field_of_study`/`tags` already exists and takes over, the admin won't understand why their provided values were ignored


## ✅ Completed
- Transaction code fix (temporary + permanent)
- University name+abbreviation search — Shahwaiz
	- Program and scholarship listing interweaving results — Shahwaiz

---

## Ideas


---
## Tech Debt
- Support Chat should be separated from the admin-chat workflow