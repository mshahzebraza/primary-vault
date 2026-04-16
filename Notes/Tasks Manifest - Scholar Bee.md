---
organization: "[[scholarbee]]"
categories:
  - "[[Work]]"
  - "[[Tasks]]"
type:
  - "[[Task]]"
status:
  - active
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
- [x] [Transcript and ID Card Fields Are Not Mandatory in Application Form](https://scholarbee-team.atlassian.net/browse/SB-1417)
- [ ] [[260416T1704 (Thu) - Add Session(Intake) Term(Season) & Year Information]]

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
- [ ] CMS Field of 'Admission Session' needs to be added - Data Entry team will handle it themselves
- [ ] SEO title key and short name be added for remaining items
- [ ] Campus Slug to be updated only based on the title
## ⚠️ Blocked
- Review Shahwaiz Chat Socket Testing Video
	- Blocked; pending on Shahwaiz
- Timezone Filtering
	- Blocked; needs discussion
	- If frontend handles timezone conversion, backend date-only APIs will be offset; need decision

## ✅ Completed
- Transaction code fix (temporary + permanent)
- University name+abbreviation search — Shahwaiz
	- Program and scholarship listing interweaving results — Shahwaiz

---
## Ideas/Future Requirements
- [ ] Chat support observability and delayed-response alerting features.
- [ ] Draft issues to be shown in the UI
	- [ ] Without Dates - might conflict with dates and tags
### Delayed Reply Observability
- [ ] Track and surface observability of delayed chat replies
- [ ] Send reminder emails to support persons for delayed replies
- [ ] Send reminders via WhatsApp to individual support persons as well
- [ ] Add analytics around delayed response times
### Student Chat UX
- [ ] Show an unavailability fallback message in the student chat when support is offline
---
## Tech Debt
- Support Chat should be separated from the admin-chat workflow