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
- [ ] [[260428T1004 (Tue) BUG - Notifications for recent admission programs not generated in db]] (Not Pushed)
- [ ] [[260428T1104 (Tue) Bug - Scheduled Emails are not sent to admins regarding missed replies]] (Not Pushed)
- [ ] Favourites API isn't sending the resolved statuses for the `receiving_applications` and `status` properties across the admission program and admission.
- [ ] **BUG:** Chat Messages Not working in the dev portal ([Jira Ticket Link](https://scholarbee-team.atlassian.net/browse/SB-1227))
	- [ ] Ask shawaiz to run the chat confirmation cycly in local development
- [ ] **Enhancement:** use a reusable frontend url link for media domain for email templates, instead of always sending the same link. 
	- [ ] Instead of putting the redirect url to the exact frontend page, redirect the user to `frontend-domain/redirects?redirect_type=signup-email-confirmation`. For example, redirect the chat messages action button from emails to a generic REDIRECTS page, that maintains a mapping of redirect-type to frontend-route.
- [x] [Transcript and ID Card Fields Are Not Mandatory in Application Form](https://scholarbee-team.atlassian.net/browse/SB-1417)
- [x] [[260416T1704 (Thu) Admission Program Details - Session Term Filtering & "Latest Term" Query Parameter]]
- [x] [[260420T1904 (Mon) Update Admission Program Filtering - Replace University Slug with Campus Slug]]
## 🟥 Pending
- [ ] Favourite program notification
- [ ] [[260424T1736 (Fri) Task - Signup parity for Google OAuth callback (required fields)]]
	- [ ] Ensure required signup fields remain required for Google signup too
	- [ ] Frontend intercepts OAuth callback and forces completion flow when required fields missing
	- [ ] Backend rejects incomplete Google signup payloads (no OAuth bypass)
- [ ] [[260424T1736 (Fri) Task - Admission status offload to frontend (derive openSoon etc)]]
	- [ ] Backend accepts only value-based filters (no derived buckets like openSoon/closingSoon)
	- [ ] Frontend derives UI state labels from dates/flags/status (covers edge cases)
- [ ] [[260424T1736 (Fri) Task - Backend: admission dates + receivingApplication + status (rich filters + app draft/submit)]]
	- [ ] Rich filters API (`withFilters`) returns correct admission programs across admission dates + receivingApplication + status (+ edge cases)
	- [ ] Application draft creation + submission enforce the same combined rules as listing
- [ ] [[260424T1736 (Fri) Task - CMS portal strict validation for admissions receivingApplication fields]]
	- [ ] Strict validation on admission start/end dates + status + receivingApplication fields
	- [ ] Disallow setting receiving application plan when `receivingApplication=false`
- [ ] Search Listing to conform to the requirements criteria submitted by the [[SB Outreach Team]]
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
- [x] [[260425T1351 (Sat) Task - Onboarding preferences + self-update endpoint]]

---
## Ideas/Future Requirements
- [ ] Chat support observability and delayed-response alerting features.
- [ ] Draft issues to be shown in the UI
	- [ ] Without Dates - might conflict with dates and tags
### Delayed Reply Observability
- [ ] Track and surface observability of delayed chat replies
- [ ] [[260423T1104 (Thu) Send reminder emails to support persons for delayed replies|Nightly email — unread student messages (all admins, inc. support)]]
- [ ] Send reminders via WhatsApp to individual support persons as well
- [ ] Add analytics around delayed response times
### Student Chat UX
- [ ] Show an unavailability fallback message in the student chat when support is offline
---
## Tech Debt
- Support Chat should be separated from the admin-chat workflow