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
related-tasks:
  - "[[260423T0904 (Thu) Timezone Dropdown List adjustments based on Daylight Savings]]"
  - "[[260423T1204 (Thu) Task - Integrate transfer ownership action in team settings view]]"
---

## Context
> We need to find and mark bugs for removal later. 

## Action Items/Bugs
### Feature Specific
#### Non Specific

- [ ] Add an optional OS Pill distinction b/w AMD, and ARM. (Might be able to use a absolute positioned pill). 

- [ ] Refactor the logic of hooks into a consolidated hook with multiple smaller hooks related to each of the functions like dialog, deletion, dialog, transfer ownership for the team settings view.  

- [ ] [ID: 10] Need - Task - LiveShell Audit Logging
  - As minimal as possible, just to check a box

- [ ] [ID: 32] Trivial - Bug - Minor weird activity with account access
  - See the loom, hard to explain – the only one I could repro was that a user could login with creds that had no workspaces...which isnt a problem I dont think, just odd? Here is the overly long loom: https://www.loom.com/share/5afb3c17897b4e2ea1ef2f782144e7bc

- [ ] [ID: 43] Need/Nice - Bug - Custom Extensions target agent group selection
  - Idk if this is a bug or more a design flaw – groups cannot be selected for extension deployment since its always 1:1. However, I literally tried making an agent group with ONE agent in it, and it generates the error 'Only connected agents can be selected for deployment'. 100% a bug, and broken.

- [ ] [ID: 44] Trivial - Bug - Custom extension deployment per group or device select is inverted?
  - Super obscure – BUT if you go to Actions > Deploy Extension and click the select option, the oldest extensions show up first, and the newest show up last. It should like be the inverse.

- [ ] [ID: 45] Need - Bug - There is no way to add agents to an existing static group in the UI
  - Prob more an oversight/task than bug – and I literally never realized until now, but if create a static agent group, and then want to add devices to that group, there is LITERALLY no way of doing that in the UI currently.

- [x] [ID: 27] Nice - Bug - Auto log out if ONE tab is inactive, even if using another tab (**QA Failed**)
  - **QA failed** in prod for normal timeout
  - Minor but kinda annoying, if I am working on tab A and B, but then if I have tab C and I am not using that, it can kick me out of the console across all tabs – can cause issues when using querysmith and stuff

- [x] [ID: 30] Trivial - Bug - On Settings > Invite Page – toast issue on existing user
	- **QA failed**
	- Genuinely might not even want to worry about this – beyond trivial. Basically, the failed invite is PERFECT – that is what we want to happen. BUT the error toast says 'Invite Created – Failed to send invite'. That is weird, it should say invite failed – and ideally say say something like 'Invite Failed – User exists' or something.

- [x] [ID: 24] Nice - Bug - Refresh not showing toast on Settings > Team page
  - **QA failed**
  - the literal button is not showing a refresh toast – confirmed it IS refreshing, just no toast

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


- [x] [ID: 22] Need - Bug - [[260423T0904 (Thu) Timezone Dropdown List adjustments based on Daylight Savings]]
  - i.e. now EST is -4 UTC, on nov 1 2026 goes back to -5... currently is -4 and says -5


- [x] [ID: 26] Nice - Bug - Remove (Default) from the Role on the frontend on Settings > Team
  - SO minor, but remove (Default) for now, since they are ALL default


- [x] [ID: 33] Need/Nice - Bug - On Settings > API Keys – few oddities, one real bug
  - Oddities: Expire pill is too close to the API Key Field. Only 2 keys allowed per role... not a problem, but wanted to note since I was not sure if that is expected. The default expiration date when creating a Key OR an API Role is today – it should default to some time in the future. Bug: If I set an API Key Expiration date <=3 days in the future, it will show expired. We don't need the expires soon if we dont want, we just cant have it say expired when it is not expired. Loom: https://www.loom.com/share/4dd44859c3fa47d994d74a34e1141c6e

- [x] [ID: 36] Trivial - Bug - Duplicate 'close' button
  - If you go to Query Pack Presets OR Assessment Templates then go to [Actions > View Details] there are 2 'Close' buttons at the bottom, and both work lol. purely cosmetic. So, Query Pack Data View's Edit and Create Dialog has 2 close buttons.

- [x] [ID: 37] Trivial - Bug - No MST in the timezone? 
  - There is techincally not a Mountain time (MST) in the timezone selection options – I know this is nuanced and minor, but there is ONE entry that between PST (Los_Angeles) and CST (Chicago), but unfortunately that is Arizona

- [x] [ID: 42] Need - Bug - LiveShell naming convention incorrect
  - Likely not a bug, but think its kinda important to note: we have LiveShell spelled differently in different parts of the tool ('Live shell', 'Liveshell', 'LiveShell'). I think we need to standardize to one, or at the very least one word vs two words. Personally, I would say LiveShell.

- [x] Remove the Mitre Link in Yara Mode. Replace it with - YARA Docs –  with this link: https://yara.readthedocs.io/en/stable/
- [x] Update Link in Windows Event Log Mode (Or add it as a Second Link: *Windows Event Catalog*. Rename the existing one as *Window Security Events*). Use this link: https://detection.wiki/
- [x] Need to update the yara mode text blurb: "Please specify what binary attributes, or contents, you wish AI to generate a yara-based query on, and the desired operating system...(e.g. Social Security Numbers in files on Windows User Desktops)"

- [x] [ID: 2] Need - Task - Remove unneeded FFs/Move to internal
  - See prior discussions/team meeting for full summary

- [x] [ID: 7] Need/Nice - Task - Remove attack group/name mode from the UI
  - its useless, so just remove it, and I can remove from the code

- [x] [ID: 8] Need/Nice - Task - Change attack to be MITRE TID & make Yara be its own mode
  - All of these at the top-level, so that there are not sub modes – no API changes needed currently, as we discussed on brief sync on the 14th

- [x] [ID: 9] Need - Task - Change 'compliance' mode to always say 'Vulnerability'
  - As mentioned on calls

- [x] [ID: 14] Need/Nice - Bug - [[260419T1504 (Sun) BUG - query editor gives UI jerk when content in the editor is too much due to a resizing change added earlier]]
  - When you save somethign as a preset on the create query page, the SQL box is massive and looks strange. If you type anything in the box it auto scales to the correct size, but is odd and def a bug currently

- [x] [ID: 23] Nice - Bug - Point rapid response 'Need Help?' link to rapid response page
  - Currently points to create query – needs to point to https://docs.aiquery.io/rapid-response

- [x] [ID: 25] Nice - Bug - On settings > Team page – search seems to be broken
  - If you search anything on the team page, it seems to not be working? here is the request url: `https://ppe-api.aiquery.io/memberships/tenant/tnt_kjFNB8kJkl1fI6iv6e-84-qqt?filters%5Buser.name%5D%5Bregex%5D=Nick&limit=10&page=1&populate=tenant%2Cuser%2Croles&sort%5Bcreated_at%5D=-1&user.name%5Bregex%5D=Nick`

- [x] [ID: 28] Nice - Bug - On settings > Invite page – search is broken also
  - BUT honestly not even needed for this page... so if you want to fix with the same way as the team search (item 25 on list) then cool, but also can just remove the search from this page

- [x] [ID: 29] Need/Nice - Bug - On Settings > Invite Page – when you click into 'Actions', the order needs to be changed for options/delete should be red
  - The order should be; Refresh, Resend, Delete. Additionally, make 'Delete' red, so that it aligns with everything in the console... only putting it as need/nice so there arent accidental deletions

- [x] [ID: 31] Trivial - Bug - On Settings > Invite Page – no refresh button
  - SO minor, but there just isnt a refesh on this page, but is on others – totally not needed though, adding this as the lowest priority
#### Rapid Response Item Actions
- [x] Save the rapid response history data as well
- [x] Save the name of Device in the history context
- [x] Point rapid response 'Need Help?' link to rapid response page: https://docs.aiquery.io/rapid-response/rapid-response-overview
