---
type: "[[Journal]]"
categories:
  - "[[Journal]]"
date:  2026-05-08
---

## Scratch
## Scholarbee
- Shawaiz meeting legal doc & requirments along with WIP of scope/applicability and document-type/categories
- discussion with Arslan on whether these pseudo tags should be computed on FE or BE

### Task: Admission Session Deduplication for same session term
Prompt In-Progress:
```
Currently, we have the relation for admission program and program collection such that any program, when connected with any admission document, creates a new entity called admission program. An admission can be connected with multiple programs, meaning that multiple programs can be opened as admission programs within the same admission session. The problem is that the admission session or admission document can be of different sessions like fall, spring, winter, etc. And ideally, if a program was created in the session fall 2025 as an admission program, and a new admission program is created from the same program document in the fall 2026, the previous document—or the previous admission program document, more precisely—is not supposed to be shown to the user. Which means that, at any given time for the same session term, only one admission program from the same program should be shown to the user. This means that if, let's say, I've created an admission program for the fall 2026 for the program of CS of campus XYZ and I published it.  


...
```
### Daily Scrum Meeting
- Should Pseudo State Computation be on Frontend or Backend?
- 