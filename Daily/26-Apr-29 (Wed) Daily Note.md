---
type: "[[Journal]]"
categories:
  - "[[Journal]]"
date:  2026-04-29
---

## Scratch
## Scholarbee Updates
- was supposed to work on the 
	- Bug: Scheduled emails to campuses not sent for missed replies issue (**Not Done**)
	- Refactor: Backfilling of notifications for admission programs against which no notification was present (**Not Done**)
- however, had a meeting in first half with Arsalan and Aliza.
	- agenda: campus slug was missing in user's favorite admission programs list
	- conclusion: meeting lasted 45-50 minutes, and the field was already available in the api response. No change from backend was required upon investigation.
- moreover, the scrum lasted fro 2PM to 4PM. Issues and Bugs were discussed.
	- Bug: Admission program detail list api was updated to sort the admissoin programs with latest admissions on top based on year (not handling sessions still).
	- Bug (QA Fail): QA said no notifications for the last day (when notification fix was implemented) were generated. This was investigated as well and found to be a testing process issue. Upon fixing the issue, the PR Review Channel was notified the updated behavior of admission program notifications that notifications will not be generated unless the Admission Program can actually receive applications. QA was educated about the fact and retesting the notifications confirmed the testing process flaw. No Change added from backend.
	- Re-Indexing of elastic search, migration of data from dev to prod was done as well.
- Another joint meeting with Student Team, Data Team, Aliza and Sharjeel was conducted as well (started at 4:00PM; immediately after Scrum)
- 