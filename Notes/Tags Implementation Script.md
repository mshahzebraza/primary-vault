---
status: active
tags:
  - task
  - script
original_path: Notes/Work/scholarbee/Tasks/Tags Implementation Script.md
base: Work
organization: "[[scholarbee]]"
path_area: Tasks
categories:
  - "[[Work]]"
  - "[[scholarbee]]"
  - "[[Tasks]]"
---

## Overview
Script to generate and assign canonical program template tags to existing programs using an LLM (Gemini). Normalizes program names, infers degree level, field of study, and tags from raw program data.

## Current Status
- Script written (v2 — New Script), improved prompt over v1 (Old Script)
- Needs to be studied and executed on the dev DB before running on prod

## Key Design Decisions
- Tag categories: `FIELD`, `LEVEL`, `TYPE`, `SPECIALIZATION` (defined as constants)
- Degree levels: Associate, Bachelor, Master, Doctorate, Diploma, Certificate
- LLM prompt instructs: return only JSON array, no markdown, merge near-duplicates
- `response_mime_type: "application/json"` enforced in Gemini config
- Pass 1 processes batches; merges near-duplicates (e.g. "BS CS" and "B.S. Computer Science" → one template)

## Script Location
> Code lives in the scholarbee repo. Search for `DEGREE_LEVELS` or `TAG_CATEGORIES` constants.

## Tasks
- [ ] Study the script thoroughly
- [ ] Run on dev DB and validate output
- [ ] Review and correct any mis-tagged templates manually
- [ ] Run on prod DB once dev run is validated

## Open Issues (surfaced during testing)
- Support chat issue: QA user (qa.student.032@test.com) not seeing support chat in conversations → investigate separately
- Ali issue: `GET /admission-programs/slug/...` returning 400 — `ResourceProtectionGuard` not applied to route → investigate separately; likely unrelated to this script

## Related Meetings
