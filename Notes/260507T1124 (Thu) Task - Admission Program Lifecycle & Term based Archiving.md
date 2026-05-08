---
type: "[[Task]]"
categories:
  - "[[Work]]"
  - "[[Tasks]]"
organization:
  - "[[scholarbee]]"
projects:
  - "[[sb-backend]]"
status: backlog
priority: P2
date: 2026-05-07
tags:
  - admission-programs
  - listing-api
  - session-deduplication
related-meetings:
  - "[[260507T1105 (Thu) Daily Note]]"
  - "[[260508T1431 (Fri) Daily Note]]"
---
## Overview

The admission program listing API should be updated so that when multiple admission programs exist for the same program at the same campus/university across different admission sessions, only the one belonging to the **newest session** is surfaced. For example, if CS at Campus XYZ exists for both Fall 2025 and Spring 2026, the Fall 2025 entry should be suppressed in favour of the Spring 2026 one. The exact implementation approach and edge cases (e.g. overlapping sessions, multiple campuses, draft programs) are pending a meeting with the product owner.
## Prompt
Prompt v1 (Submitted to cms-portal llm):
```
### Feature Implementation: Admission Program Lifecycle & Archiving Logic

**1. Background & Data Model**
Currently, our system creates a junction entity called an `Admission Program` when a base `Program` is connected to a specific `Admission` session. An `Admission` session can be of different terms (e.g., Fall, Spring, Winter). 

*Base Example:*
* Fall 2025 Admission + CS Campus ABC = `CS Fall 2025 Campus ABC`
* Spring 2025 Admission + CS Campus ABC = `CS Spring 2025 Campus ABC`
* Fall 2026 Admission + CS Campus ABC = `CS Fall 2026 Campus ABC`

**2. Primary Objective**
At any given time, the front-end should ideally display only **one** active `Admission Program` per base `Program` **for a specific session term**. 

This means a program can have an active "Fall" session and an active "Spring" session simultaneously, but it should never display two active "Fall" sessions for the same program (unless an overlap period is actively occurring). To support this, we need to introduce an `Archived` status and automate the transition of older documents to this state based on chronological sessions and session terms.

**3. Core Business Rules**

* **Status Implementation:** Implement the `Archived` status for the `Admission Program` collection.
* **Auto-Archiving on Creation/Publishing (Term-Specific):** When a *subsequent* (newer) `Admission Program` is published for a specific base `Program` and session term (e.g., Fall), the system must check the *prior* (older) `Admission Program` **of that exact same session term**. The prior document should automatically be set to `Archived` **ONLY IF**:
  * Its status is currently `Published`.
  * Its deadline is defined.
  * Its deadline has expired based on the current date/time.
* **The Overlap Exception:** If the prior `Admission Program` is still `Published`, has no deadline, or its deadline has not yet expired, **do not archive it**. Both the prior and subsequent admission programs of that term will remain active and visible to the user until the prior one naturally expires.
* **Publishing Validation (Guardrail):** Implement a validation check to prevent backward publishing. If a data entry user attempts to publish a draft of a *prior* session's `Admission Program`, the system must throw an error if a *subsequent* session's `Admission Program` **for the same term** is already published.

**4. Workflow Examples**

To clarify the business rules, here is how the system should handle specific scenarios:

* **Scenario A (Different-Term Coexistence):** `CS Fall 2025` is published. An admin then publishes `CS Spring 2025`. Because they belong to different session terms, no archiving is triggered. Both remain `Published` and visible to users.
* **Scenario B (Same-Term Archiving):** Following Scenario A, `CS Fall 2025` and `CS Spring 2025` are both active. Later, an admin publishes `CS Fall 2026`. The system checks for prior programs with the "Fall" term. It finds `CS Fall 2025`, sees its deadline has passed, and archives it. `CS Spring 2025` is untouched and remains active.
* **Scenario C (The Overlap Exception):** `CS Fall 2025` is published with a deadline of Nov 30th. On Nov 15th, an admin publishes `CS Fall 2026`. The system checks `CS Fall 2025`, but sees the deadline has *not* passed yet. Both `CS Fall 2025` and `CS Fall 2026` remain `Published` and visible to users.
* **Scenario D (Guardrail Block):** `CS Fall 2026` is already published and active. An admin finds an old `Draft` of `CS Fall 2025` and clicks Publish. The system blocks the action and throws an error: *"Cannot publish a prior admission program because a subsequent session for this term is already active."*

**5. Background Worker (Cron Job)**

Because of the "Overlap Exception" (Scenario C), a prior program will stay active alongside a subsequent program. We need a daily (or hourly) cron job to clean up these overlaps once the prior program finally expires. 

* **Cron Job Workflow:** Following Scenario C above, the calendar rolls over to Dec 1st. The cron job runs, finds that `CS Fall 2025` (deadline Nov 30th) is now expired. It checks and sees `CS Fall 2026` exists for the same base program **and the same term**. The cron job safely updates `CS Fall 2025` to `Archived`.

**6. Task & Action Required**
Please review this architecture and provide the implementation for the logic, validations, and cron job. Additionally, act as a system architect and analyze this flow for edge cases. Highlight any potential vulnerabilities or logical flaws (for example: how do we chronologically sort "prior" vs "subsequent" sessions reliably in the database, and how exactly is the "term" matched?) and propose robust solutions to handle them.

```


- Prompt v2 (for backend - highlights admission level issues)
```
### Feature Implementation: Admission Program Lifecycle, Archiving Logic & Bulk Operations

**1. Background & Data Model**
Currently, our system creates a junction entity called an `Admission Program` when a base `Program` is connected to a specific `Admission` session. An `Admission` session can be of different terms (e.g., Fall, Spring, Winter) and acts as a parent document to multiple programs.

*Base Example:*
* Fall 2025 Admission + CS Campus ABC = `CS Fall 2025 Campus ABC`
* Spring 2025 Admission + CS Campus ABC = `CS Spring 2025 Campus ABC`
* Fall 2026 Admission + CS Campus ABC = `CS Fall 2026 Campus ABC`

*Crucial Architecture Note:* The standard workflow involves updating the *parent* `Admission` session. When a parent session is published or marked to "receive applications", that status cascades down, automatically updating and publishing all of its associated child `Admission Programs` in bulk.

**2. Primary Objective**
At any given time, the front-end should ideally display only **one** active `Admission Program` per base `Program` **for a specific session term**. 

Because publishing usually happens in bulk at the parent `Admission` level, the system must be capable of processing archiving rules and overlap checks at scale, ensuring data integrity across potentially hundreds of programs simultaneously during a single frontend action.

**3. Core Business Rules**

* **Status Implementation:** Implement the `Archived` status for the `Admission Program` collection.
* **Auto-Archiving on Creation/Publishing (Term-Specific & Bulk-Aware):** When a *subsequent* (newer) `Admission Program` is published (either individually or cascaded via the parent session) for a specific base `Program` and session term, the system must check the *prior* (older) `Admission Program` **of that exact same session term**. The prior document should automatically be set to `Archived` **ONLY IF**:
  * Its status is currently `Published`.
  * Its deadline is defined.
  * Its deadline has expired based on the current date/time.
* **The Overlap Exception:** If the prior `Admission Program` is still `Published`, has no deadline, or its deadline has not yet expired, **do not archive it**. Both the prior and subsequent admission programs of that term will remain active.
* **Publishing Validation (Guardrail):** Implement a validation check to prevent backward publishing. If an attempt is made to publish a *prior* session's `Admission Program` (individually or via bulk parent publish), the system must throw an error if a *subsequent* session's `Admission Program` **for the same term** is already published.

**4. Workflow Examples**

* **Scenario A (Different-Term Coexistence):** `CS Fall 2025` is published. An admin then publishes `CS Spring 2025`. Because they belong to different session terms, no archiving is triggered.
* **Scenario B (Same-Term Archiving):** `CS Fall 2025` is active. Later, an admin individually publishes `CS Fall 2026`. The system checks for prior programs with the "Fall" term. It finds `CS Fall 2025`, sees its deadline has passed, and archives it.
* **Scenario C (The Overlap Exception):** `CS Fall 2025` is published with a deadline of Nov 30th. On Nov 15th, an admin publishes `CS Fall 2026`. Both remain `Published` and visible to users because the prior deadline hasn't passed.
* **Scenario D (Bulk Publishing & Archiving):** The parent `Fall 2026 Admission` session (containing 50 programs) is published by an admin. The system iterates through all 50 programs. It finds the 50 corresponding `Fall 2025` programs. It archives the 48 that have expired, applies the "Overlap Exception" to the 2 that are still active, and successfully publishes the 50 new ones.
* **Scenario E (Bulk Guardrail Block):** `Fall 2026 Admission` is already published. An admin mistakenly clicks "Publish" on the parent `Fall 2025 Admission` session. The system must handle this gracefully, blocking the action and alerting the user that subsequent programs for this term are already active.

**5. Background Worker (Cron Job)**

Because of the "Overlap Exception" (Scenario C and D), prior programs will stay active alongside subsequent programs. We need a cron job to clean up these overlaps once the prior programs finally expire. 

* **Cron Job Workflow:** Following Scenario C, the calendar rolls over to Dec 1st. The cron job runs, finds that `CS Fall 2025` (deadline Nov 30th) is now expired. It checks and sees `CS Fall 2026` exists for the same base program **and the same term**. The cron job safely updates `CS Fall 2025` to `Archived`.

**6. Task & Action Required**
Please review this architecture and provide the implementation for the logic, validations, and cron job. Additionally, act as a system architect and analyze this flow for edge cases, particularly focusing on the **Bulk Publishing Workflow**. 

Highlight potential vulnerabilities, logical flaws, and performance bottlenecks. Please propose solutions to handle:
* **Transactional Integrity:** If 1 out of 50 programs fails the Guardrail validation during a bulk publish, does the entire parent session fail to publish, or is it partially successful? How do we handle database rollbacks in MongoDB/Mongoose to prevent corrupted UI states?
* **Chronological Sorting:** How do we reliably determine "prior" vs "subsequent" sessions in the database, and how exactly is the "term" matched?
* **Race Conditions:** Are there concurrency issues or database locking concerns if the cron job runs at the exact moment an admin hits "Bulk Publish"?
* **Performance:** How do we optimize the database queries so a bulk publish of 200 programs doesn't cause an API timeout?
```
## Current Tasks

- [ ] **Meeting:** Schedule and conduct a meeting with the product owner to finalise requirements, edge cases, and the definition of "newer session"
- [ ] **Design:** Decide on the deduplication strategy — DB-level (query), application-level filter, or ES index-time suppression
- [ ] **Edge cases to clarify in meeting:**
  - How to handle programs open in parallel across different sessions intentionally
  - Behaviour when the newer session program is in draft/inactive state
  - Whether deduplication is scoped per campus or per university
  - How this interacts with the favourites API and other listing variants (search, filters)
- [ ] **Design alternative to discuss:** Instead of filtering at query/listing time, auto-demote older session programs on the write path — when a newer session admission program is created with `receivingApplication=true`, or when an existing newer-session program is flipped to `receivingApplication=true`, automatically set `receivingApplication=false` on all older-session programs for the same program+campus. This keeps the data consistent at source rather than papering over it at read time, but requires agreement on the trigger conditions and whether the demotion should be reversible.

- [ ] **Implementation:** Update the listing API to apply the session-deduplication logic once approach is agreed
- [ ] **Testing:** Cover edge cases with integration tests (parallel sessions, draft newer session, multiple campuses)
