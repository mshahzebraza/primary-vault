---
organization: "[[scholarbee]]"
categories:
  - "[[Work]]"
  - "[[Tasks]]"
type: "[[Documentation]]"
status: active
tags:
  - orphan-tasks
  - minor-tasks
---

## Document Intent
This document is meant to document the tasks that do not warrant a dedicated document-note yet.

## Summary

| Sr. | Priority |  Status   | Title                                                                 |
| :-: | :------: | :-------: | --------------------------------------------------------------------- |
|  1  |    P1    |  Active   | [[Migrate Media Items]]                                               |
|  2  |    P1    |  Active   | [[Tags Implementation Script]]                                        |
|  3  |    P1    |  Active   | Add Draft Admission Program functionality                             |
|  4  |    P2    |  Blocked  | Review Shahwaiz Chat Socket Testing Video                             |
|  5  |    P1    |  Blocked  | Timezone Filtering                                                    |
|  6  |    P1    |  Blocked  | Chat Issue                                                            |
|  7  |    P1    |   Todo    | R&D on Elastic Search storage options                                 |
|  8  |    P1    |   Todo    | [[Future Feature Requirements]]                                       |
|  9  |    P1    |   Todo    | [[202604031318 - scholarbee tasks]]                                   |
| 10  |    P1    |   Todo    | [[urgent issues checklist]]                                           |
| 11  |    P2    |   Todo    | [[referral system setup]]                                             |
| 12  |    P2    |   Todo    | Fix & Maintain the Test User Creation Script                          |
| 13  |    P2    |   Todo    | Data Inconsistency due to missing fields                              |
| 14  |    P2    |   Todo    | [[AI Context Setup]]                                                  |
| 15  |    P1    | Completed | Slug not available in ES List                                         |
| 16  |    P1    | Completed | Accept redirect link in body of email verification API              |


### Explaination

- **Sr. 1:** [[Migrate Media Items]]
- **Sr. 2:** [[Tags Implementation Script]]
- **Sr. 3:** Add Draft Admission Program functionality
	- Add ability to create draft admission programs; hide in ES indexing and DB results
- **Sr. 4:** Review Shahwaiz Chat Socket Testing Video
	- Blocked; pending on Shahwaiz
- **Sr. 5:** Timezone Filtering
	- Blocked; needs discussion
	- If frontend handles timezone conversion, backend date-only APIs will be offset; need decision
- **Sr. 6:** Chat Issue
	- Blocked; needs devops debugging
	- `api-dev`: sockets connect, no messages sent regardless of `user_type`
	- `api-prod`: sockets not connecting
	- `api-staging`: sockets connect, admin chat broken
- **Sr. 7:** R&D on Elastic Search storage options
- **Sr. 8:** [[Future Feature Requirements|Chat Observability & Delayed Reply Alerting]]
- **Sr. 9:** [[202604031318 - scholarbee tasks|Program Creation from University Portal]]
	- Architecture unresolved
- **Sr. 10:** [[urgent issues checklist|Urgent Issues Checklist]]
- **Sr. 11:** [[referral system setup|Referral Code Architecture & Setup]]
- **Sr. 12:** Fix & Maintain the Test User Creation Script
- **Sr. 13:** Data Inconsistency due to missing fields
- **Sr. 14:** [[AI Context Setup|AI / Cursor Rules & Testing Setup]]
- **Sr. 15:** Slug not available in ES List
	- Completed: fixed (missing slug-generation logic for new CMS entries)
- **Sr. 16:** Accept redirect link in body of email verification APIg