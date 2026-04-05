---
banner_y: '0'
Status: Active
organization: '[[scholarbee]]'
categories:
- '[[Work]]'
- '[[scholarbee]]'
- '[[Tasks]]'
type: '[[Documentation]]'
---

## Legend
⏸️: Pending Status
➡️: Active Status
⏩: Delegated
🟡: P0 (Highest) Priority
🟠: P1 (Medium) Priority
🔴: P2 (Low) Priority

## Active Tasks

- ➡️ 🔴 P1: [[Migrate Media Items]]
- ➡️ 🔴 P1: [[Tags Implementation Script]]
- ➡️ 🔴 P1: Add Draft Admission Program functionality
	- Add ability to create draft admission programs; hide in ES indexing and DB results

## Blocked Tasks
- ⏸️ 🟡 P2: Review Shahwaiz Chat Socket Testing Video (pending on Shahwaiz)
- ⏸️ 🟠 P1: Timezone Filtering (blocked: needs discussion)
	- if frontend handles timezone conversion, backend date-only APIs will be offset; need decision
- ⏸️ 🟠 P1: Chat Issue (blocked: needs devops debugging)
	- `api-dev`: sockets connect, no messages sent regardless of `user_type`
	- `api-prod`: sockets not connecting
	- `api-staging`: sockets connect, admin chat broken

## Delegated Tasks

## Todo Tasks

### High Priority

### Medium Priority
- 🟠 P1: R&D on Elastic Search storage options
- 🟠 P1: [[Future Feature Requirements|Chat Observability & Delayed Reply Alerting]]
- 🟠 P1: [[202604031318 - scholarbee tasks|Program Creation from University Portal]] (architecture unresolved)
- 🟠 P1: [[urgent issues checklist|Urgent Issues Checklist]]

### Low Priority
- 🟡 P2: [[referral system setup|Referral Code Architecture & Setup]]
- 🟡 P2: Fix & Maintain the Test User Creation Script
- 🟡 P2: Data Inconsistency due to missing fields
- 🟡 P2: [[AI Context Setup|AI / Cursor Rules & Testing Setup]]

## Completed

- ⏩ 🔴 P1: Slug not available in ES List — fixed (missing slug-generation logic for new CMS entries)
- 🟠 P1: Accept redirect link in body of email verification API
