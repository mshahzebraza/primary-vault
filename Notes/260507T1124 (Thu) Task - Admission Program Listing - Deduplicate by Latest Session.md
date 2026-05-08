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
