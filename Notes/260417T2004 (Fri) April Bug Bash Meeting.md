---
type:
  - "[[Meeting]]"
  - "[[Task]]"
categories:
  - "[[Meetings]]"
  - "[[Work]]"
  - "[[Tasks]]"
date: 2026-04-19
tags:
  - bug
  - task
  - minor-tasks
organization:
  - "[[aiquery.io]]"
projects:
  - "[[aq-client]]"
  - "[[aq-backend]]"
attendees:
  - "[[Rajput]]"
  - "[[Nick]]"
status:
  - active
priority: P1
related-tasks:
  - "[[260423T0904 (Thu) Timezone Dropdown List adjustments based on Daylight Savings]]"
  - "[[260423T1204 (Thu) Task - Integrate transfer ownership action in team settings view]]"
  - "[[260425T1604 (Sat) Add Agents to existing group]]"
---

## Context
> We need to find and mark bugs for removal later.

## Action Items / Bugs

### Pending
- [ ] A single agent should be able to be moved to an agent group if required; through the row actions
- [ ] Create a variation pattern for the agent list views
- [x] Refactor the logic of hooks into a consolidated hook with multiple smaller hooks related to each of the functions like dialog, deletion, dialog, transfer ownership for the team settings view.
- [ ] [ID: 10] Need - Task - LiveShell Audit Logging
  - As minimal as possible, just to check a box
- [x] [ID: 43] Need/Nice - Bug - Custom Extensions target agent group selection
  - Groups cannot be selected for extension deployment since it is always 1:1. Making an agent group with ONE agent yields error 'Only connected agents can be selected for deployment' — incorrect error; field effectively broken for custom extension creation.
- [ ] [ID: 44] Trivial - Bug - Custom extension deployment list order inverted (+ optional AMD vs ARM pill)
  - Oldest extensions show first, newest last — should be inverse. Sheet also calls out optional pill distinction for AMD vs ARM on deploy flows. 🔥🔥
- [ ] [ID: 45] Need - Bug - [[260425T1604 (Sat) Add Agents to existing group|Add agents to an existing static group in the UI]]
  - See dedicated task note for full context/description.
- [ ] [ID: 50] Trivial - Bug - Registration Key Refresh oddity 🔥🔥🔥
  - UX not intuitive; see https://www.loom.com/share/fb9d8ea48f8647f385f4e80f9dc3542c
- [x] [ID: 55] Need - Bug - Schedule: EST timezone off when selected (DST)
  - Without timezone, local time in error message is correct; with EST selected, offset wrong (-5 vs -4 during DST). Related to timezone bugs.
- [ ] [ID: 56] Trivial - Task - Lack of OR operators when creating dynamic group 
  - Only one input per field; cannot express OR (e.g. device name contains EC2 OR nick). Low priority.
- [ ] [ID: 62] Need/Nice - Bug - Edit & rerun for expired query pack goes to Oops page
  - **No Fix from frontend required**, because eealistic solve is to remove expired / do not offer edit & rerun for expired blank packs. (Rajput/Shazeb)
- [x] [ID: 66] Nice - Bug - Query export on failed status — do not allow download
  - Status failed but user can still trigger download of non-existent file; disable download.
- [ ] [ID: 70] Nice - Bug - Delay in query results details showing
  - Minor; likely DB write latency between success and viewable results. (Rajput/Shazeb)
  - Probably from backend
- [x] [ID: 73] Need/Nice - Task - Allow AI confidence to return N/A
  - Error-handling path when confidence cannot be an int.
- [x] [ID: 74] Critical - Task - Need UI changes to support agent group move (relates to ID 45)
  - Agents > Agent List: Actions → "Add to Agent Group" → popup to select group (like version select for agent update).
  - Agent Groups > group > agent list: Actions → "Remove from Agent Group" (confirm optional); no extra group picker.
- [ ] [ID: 76] Need/Nice - Bug - Query results for removed agent returns wrong warning
  - Error: `invalid_type` at `data[0].agent` — expected object, received undefined. (Rajput/Shazeb)
- [x] [ID: 75] Nice - Bug - Minor UI hiccup (Windows Event Log mode links squished during AI "constructing query")
  - Cosmetic: second Windows Event Log link squeezes layout; consider shortening link labels (e.g. drop "Windows" — "Security Events" / "Event Catalog"). Sheet: not yet resolved.

### QA
- [x] [ID: 22] Need - Bug - [[260423T0904 (Thu) Timezone Dropdown List adjustments based on Daylight Savings]]
  - Sheet: Resolved y, Confirmed working (ppe) n — verify on PPE after deploy.
- [x] [ID: 24] Nice - Bug - Refresh not showing toast on Settings > Team page
  - Previously marked QA failed; verify toast after fix on PPE.
- [x] [ID: 27] Nice - Bug - Auto log out if ONE tab is inactive, even if using another tab
  - **QA failed** in prod for normal timeout; re-verify after fix.
- [x] [ID: 30] Trivial - Bug - On Settings > Invite Page – toast wording when user already exists
  - **QA failed**; verify copy ("Invite Failed – User exists" or similar) on PPE.
- [x] [ID: 42] Need - Bug - LiveShell naming convention incorrect
  - Sheet: Resolved y, PPE n — standardize to LiveShell (or chosen casing) and confirm in UI + userguide on PPE.
- [ ] [ID: 63] Need/Nice - Bug - Export UX annoyance
  - Sheet: Resolved y, Confirmed working (ppe) n — after export, "See Results" should show job without manual refresh; verify on PPE.
	  - ***Couldn't Test. Was getting 500 errors for exports***

### Completed
- [x] Optional: timezone selection should preferable use local TZ selection
- [x] Automatically Select the local time in the schedules dialog
- [x] UI Bug: Query SQL Input in the Query Schedule, View Detail Dialog is one-line and scrollable.
  - Take a reference from Query Pack Schedule SQL Input (it also has sql highlighting)
- [x] In API Roles Page, Expiry Pill positioning and Range is not correct
- [x] [[260423T1204 (Thu) Task - Integrate transfer ownership action in team settings view]]
  - API code block
```
{[domain}}/tenant/transfer-ownership  
body: {  
    @IsNotEmpty()  
    newRootUserId: string  
}
```
- [x] [ID: 26] Nice - Bug - Remove (Default) from the Role on the frontend on Settings > Team
- [x] [ID: 33] Need/Nice - Bug - On Settings > API Keys – few oddities, one real bug
  - Expire pill spacing; default expiry should be future; expiration <=3 days must not show as expired. Loom: https://www.loom.com/share/4dd44859c3fa47d994d74a34e1141c6e
- [x] [ID: 36] Trivial - Bug - Duplicate 'close' button
  - Query Pack Presets OR Assessment Templates (multi-query presets) → Actions > View Details: two Close buttons at bottom. Cosmetic.
- [x] [ID: 37] Trivial - Bug - No MST in the timezone?
  - Arizona vs MST nuance in dropdown between Los Angeles and Chicago.
- [x] Remove the Mitre Link in Yara Mode. Replace it with - YARA Docs – with this link: https://yara.readthedocs.io/en/stable/
- [x] Update Link in Windows Event Log Mode (Or add it as a Second Link: *Windows Event Catalog*. Rename the existing one as *Window Security Events*). Use this link: https://detection.wiki/
- [x] Need to update the yara mode text blurb: "Please specify what binary attributes, or contents, you wish AI to generate a yara-based query on, and the desired operating system...(e.g. Social Security Numbers in files on Windows User Desktops)"
- [x] [ID: 2] Need - Task - Remove unneeded FFs/Move to internal
- [x] [ID: 7] Need/Nice - Task - Remove attack group/name mode from the UI
- [x] [ID: 8] Need/Nice - Task - Change attack to be MITRE TID & make Yara be its own mode
- [x] [ID: 9] Need - Task - Change 'compliance' mode to always say 'Vulnerability'
- [x] [ID: 14] Need/Nice - Bug - [[260419T1504 (Sun) BUG - query editor gives UI jerk when content in the editor is too much due to a resizing change added earlier]]
- [x] [ID: 23] Nice - Bug - Point rapid response 'Need Help?' link to rapid response page
- [x] [ID: 25] Nice - Bug - On settings > Team page – search seems to be broken
- [x] [ID: 28] Nice - Bug - On settings > Invite page – search is broken also
- [x] [ID: 29] Need/Nice - Bug - On Settings > Invite Page – Actions menu order; Delete should be red
- [x] [ID: 31] Trivial - Bug - On Settings > Invite Page – no refresh button
#### Rapid Response Item Actions
- [x] Save the rapid response history data as well
- [x] Save the name of Device in the history context
- [x] Point rapid response 'Need Help?' link to rapid response page: https://docs.aiquery.io/rapid-response/rapid-response-overview

---

## Reconciliation notes (Google Sheet vs this meeting)

**Added from sheet** (were missing here): [ID: 50], [ID: 55], [ID: 56], [ID: 62], [ID: 66], [ID: 70], [ID: 73], [ID: 74], [ID: 75], [ID: 76]. **[ID: 63]** was missing as a line item; it is **Resolved y** on the sheet — listed under **QA** (PPE confirmation pending), not under Pending.

**Already aligned with sheet** (kept, possibly moved section): [ID: 10], [ID: 22], [ID: 24], [ID: 27], [ID: 30], [ID: 33], [ID: 36], [ID: 37], [ID: 42], [ID: 43], [ID: 44], [ID: 45].

**Meeting-only items** (not in the sheet snippet — kept as engineering / bug-bash carryover): hook refactor for team settings; transfer ownership integration note; optional timezone / schedule dialog / query schedule SQL one-liner; API Roles expiry pill fix; Rapid Response history bullets; Yara/Mitre/link copy items without sheet IDs; query mode tasks [ID: 2,7,8,9]; team/invite search [25,28,29,31]; items [14,23] and related task links.

**Merged for sheet alignment**: Standalone "AMD vs ARM pill" line was merged into **[ID: 44]** per sheet row 44 wording.
