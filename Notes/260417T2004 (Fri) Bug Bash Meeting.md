---
type:
  - "[[Meeting]]"
  - "[[Task]]"
categories:
  - "[[Personal]]"
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
---

## Context
> We need to find and mark bugs for removal later. 

## Action Items/Bugs
### Feature Specific
#### Rapid Response Item Actions
- [x] Save the rapid response history data as well
- [x] Save the name of Device in the history context
- [x] Point rapid response 'Need Help?' link to rapid response page: https://docs.aiquery.io/rapid-response/rapid-response-overview

### Non Specific
- [ ] Remove the Mitre Link in Yara Mode. Replace it with - YARA Docs –  with [this link](https://yara.readthedocs.io/en/stable/)
- [ ] Update Link in Windows Event Log Mode (Or add it as a Second Link: *Windows Event Catalog*. Rename the existing one as *Window Security Events*)
- [ ] Need to update the yara mode text blurb
	- "Please specify what binary attributes, or contents, you wish AI to generate a yara-based query on, and the desired operating system...(e.g. Social Security Numbers in files on Windows User Desktops)"
- [ ] Optional: timezone selection should preferable use local TZ selection
- [ ] Daylight Saving Timezone Issue (Need to Swap automatically; Look for better solution)
		- [ ] Second Sunday march moves forwards New York is -4
		- [ ] First Sunday in november go back to New York is -5
- [ ] Keep the logout on inactivity consider the activity on other tabs before logging user our

- [x] **[ID 2] Remove unneeded FFs/Move to internal**
  - **Category:** Task | **Severity:** Need 
  - **Comments:** See prior discussions/team meeting for full summary

- [x] **[ID 7] Remove attack group/name mode from the UI**
  - **Category:** Task | **Severity:** Need/Nice
  - **Comments:** its useless, so just remove it, and I can remove from the code

- [x] **[ID 8] Change attack to be MITRE TID & make Yara be its own mode**
  - **Category:** Task | **Severity:** Need/Nice
  - **Comments:** All of these at the top-level, so that there are not sub modes – no API changes needed currently, as we discussed on brief sync on the 14th

- [x] **[ID 9] Change 'compliance' mode to always say 'Vulnerability'**
  - **Category:** Task | **Severity:** Need
  - **Comments:** As mentioned on calls

- [ ] **[ID 10] LiveShell Audit Logging**
  - **Category:** Task | **Severity:** Need
  - **Comments:** As minimal as possible, just to check a box

- [x] **[ID 14] [[260419T1504 (Sun) BUG - query editor gives UI jerk when content in the editor is too much due to a resizing change added earlier]]**
  - **Category:** Bug | **Severity:** Need/Nice
  - **Comments:** When you save somethign as a preset on the create query page, the SQL box is massive and looks strange. If you type anything in the box it auto scales to the correct size, but is odd and def a bug currently

- [ ] **[ID 19] Need to update the yara mode text blurb**
  - **Category:** Task | **Severity:** Nice
  - **Comments:** Nick to provide blurb to Shazeb

- [ ] **[ID 20] Update Link in Windows Event Log Mode**
  - **Category:** Task | **Severity:** Nice
  - **Comments:** Super minor, but think this link is better than the one we have now: https://detection.wiki/

- [ ] **[ID 21] Create one page PDF of ins**
  - **Category:** Task | **Severity:** Need
  - **Comments:** Will give you updated link to reference (or just remove)

- [ ] **[ID 22] Timezone adjustments based on Daylight Savings**
  - **Category:** Bug | **Severity:** Need
  - **Comments:** i.e. now EST is -4 UTC, on nov 1 2026 goes back to -5...currently is -4 and says -5

- [ ] **[ID 23] Point rapid response 'Need Help?' link to rapid response page**
  - **Category:** Bug | **Severity:** Nice
  - **Comments:** Currently points to create query – needs to point to https://docs.aiquery.io/rapid-response

- [ ] **[ID 24] Refresh not showing toast on Settings > Team page**
  - **Category:** Bug | **Severity:** Nice
  - **Comments:** the literal button is not showing a refresh toast – confirmed it IS refreshing, just no toast

- [ ] **[ID 25] On settings > Team page – search seems to be broken**
  - **Category:** Bug | **Severity:** Nice
  - **Comments:** If you search anything on the team page, it seems to not be working? here is the request url: `https://ppe-api.aiquery.io/memberships/tenant/tnt_kjFNB8kJkl1fI6iv6e-84-qqt?filters%5Buser.name%5D%5Bregex%5D=Nick&limit=10&page=1&populate=tenant%2Cuser%2Croles&sort%5Bcreated_at%5D=-1&user.name%5Bregex%5D=Nick`

- [ ] **[ID 26] Remove (Default) from the Role on the frontend on Settings > Team**
  - **Category:** Bug | **Severity:** Nice
  - **Comments:** SO minor, but remove (Default) for now, since they are ALL default

- [ ] **[ID 27] Auto log out if ONE tab is inactive, even if using another tab**
  - **Category:** Bug | **Severity:** Nice
  - **Comments:** Minor but kinda annoying, if I am working on tab A and B, but then if I have tab C and I am not using that, it can kick me out of the console across all tabs – can cause issues when using querysmith and stuff

- [ ] **[ID 28] On settings > Invite page – search is broken also**
  - **Category:** Bug | **Severity:** Nice
  - **Comments:** BUT honestly not even needed for this page...so if you want to fix with the same way as the team search (item 25 on list) then cool, but also can just remove the search from this page

- [ ] **[ID 29] On Settings > Invite Page – when you click into 'Actions', the order needs to be changed for options/delete should be red**
  - **Category:** Bug | **Severity:** Need/Nice
  - **Comments:** The order should be; Refresh, Resend, Delete. Additionally, make 'Delete' red, so that it aligns with everything in the console...only putting it as need/nice so there arent accidental deletions

- [ ] **[ID 30] On Settings > Invite Page – toast issue on existing user**
  - **Category:** Bug | **Severity:** Trivial
  - **Comments:** Genuinely might not even want to worry about this – beyond trivial. Basically, the failed invite is PERFECT – that is what we want to happen. BUT the error toast says 'Invite Created – Failed to send invite'. That is weird, it should say invite failed – and ideally say say something like 'Invite Failed – User exists' or something.

- [ ] **[ID 31] On Settings > Invite Page – no refresh button**
  - **Category:** Bug | **Severity:** Trivial
  - **Comments:** SO minor, but there just isnt a refesh on this page, but is on others – totally not needed though, adding this as the lowest priority

- [ ] **[ID 32] Minor weird activity with account access**
  - **Category:** Bug | **Severity:** Trivial
  - **Comments:** See the loom, hard to explain – the only one I could repro was that a user could login with creds that had no workspaces...which isnt a problem I dont think, just odd? Here is the overly long loom: https://www.loom.com/share/5afb3c17897b4e2ea1ef2f782144e7bc

- [ ] **[ID 33] On Settings > API Keys – few oddities, one real bug.**
  - **Category:** Bug | **Severity:** Need/Nice
  - **Comments:** **Oddities:** Expire pill is too close to the API Key Field. Only 2 keys allowed per role...not a problem, but wanted to note since I was not sure if that is expected. The default expiration date when creating a Key OR an API Role is today – it should default to some time in the future. **BUG:** If I set an API Key Expiration date <=3 days in the future, it will show expired. We don't need the expires soon if we dont want, we just cant have it say expired when it is not expired. **LOOM:** https://www.loom.com/share/4dd44859c3fa47d994d74a34e1141c6e

- [ ] **[ID 34] Reset Password email went to spam (other invite emails DO NOT go to spam?)**
  - **Category:** Other | **Severity:** Nice
  - **Comments:** Just kind of odd and wanted to note – also the toast says that its coming from noreply@aiquery.io – but the email actually came from noreply@aiquery-dev.firebaseapp.com, while the tenant invite comes from admin@aiquery.io?

- [ ] **[ID 35] SQL box resizing issue on query schedules, packs, and templates**
  - **Category:** Bug | **Severity:** Need/Nice
  - **Comments:** Def the same bug as ID 14, since its the same form, just wanted to note down

- [ ] **[ID 36] Duplicate 'close' button**
  - **Category:** Bug | **Severity:** Trivial
  - **Comments:** If you go to Query Pack Presets OR Assessment Templates then go to [Actions > View Details] there are 2 'Close' buttons at the bottom, and both work lol. purely cosmetic

- [ ] **[ID 37] No MST in the timezone**
  - **Category:** Bug | **Severity:** Trivial
  - **Comments:** There is techincally not a Mountain time (MST) in the timezone selection options – I know this is nuanced and minor, but there is ONE entry that between PST (Los_Angeles) and CST (Chicago), but unfortunately that is Arizona

- [ ] **[ID 42] LiveShell Naming convention incorrect**
  - **Category:** Bug | **Severity:** Need
  - **Comments:** Likely not a bug, but think its kinda important to note: we have LiveShell spelled differently in different parts of the tool ('Live shell', 'Liveshell', 'LiveShell'). I think we need to standardize to one, or at the very least one word vs two words. Personally, I would say LiveShell.

- [ ] **[ID 43] Custom Extensions Target Agent Group Selection**
  - **Category:** Bug | **Severity:** Need/Nice
  - **Comments:** Idk if this is a bug or more a design flaw – groups cannot be selected for extension deployment since its always 1:1. However, I literally tried making an agent group with ONE agent in it, and it generates the error 'Only connected agents can be selected for deployment'. 100% a bug, and broken.

- [ ] **[ID 44] Custom extension deployment per group or device select is inverted?**
  - **Category:** Bug | **Severity:** Trivial
  - **Comments:** Super obscure – BUT if you go to Actions > Deploy Extension and click the select option, the oldest extensions show up first, and the newest show up last. It should like be the inverse.

- [ ] **[ID 45] THERE IS NO WAY TO ADD AGENTS TO AN EXISTING STATIC GROUP IN THE UI**
  - **Category:** Bug | **Severity:** Need
  - **Comments:** Prob more an oversight/task than bug – and I literally never realized until now, but if create a static agent group, and then want to add devices to that group, there is LITERALLY no way of doing that in the UI currently.



#### Team Page
- Refresh on team view doesn't show toast
- search doesn't work on team page
	- dual filters on team table page, i.e. `filters[user.name][regex]` and `user.name[regex]` filters
- role text for system roles should not include `(Default)` 
- 
