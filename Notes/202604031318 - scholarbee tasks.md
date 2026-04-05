---
date: 2026-04-03
tags:
- task
original_path: Notes/Work/scholarbee/Tasks/202604031318 - scholarbee tasks.md
base: Work
organization: '[[scholarbee]]'
path_area: Tasks
categories:
- '[[Work]]'
- '[[scholarbee]]'
- '[[Tasks]]'
type: '[[Task]]'
projects: []
priority: P2
---

## Completed
- ✅ Transaction code fix (temporary + permanent)
- ✅ University abbreviation search — Shahwaiz
- ✅ Program and scholarship listing interweaving results — Shahwaiz

## Blocked / In Progress
- ⚠️ Search listing ranking issue
- ⚠️ Existing application snapshot data — media links broken
- ⚠️ Commit the program template data from data entry into the database

## Pending
- [ ] Favourite program notification
- [ ] Review the program creation flow outside the admin CMS (from university portal)
- [ ] University dropdown lookup should search against both abbreviation and name

## Unresolved — Program Creation from University Portal
Architecture decisions still needed:

- Should university admins be allowed to **create** program templates directly, or only **request** creation (requiring super-admin approval)?
  - If allowed: a lookup API must be provided matching against `abbreviation`, `name`, and `field_of_study`

- If direct creation is allowed, how do we prevent race conditions creating duplicate templates with the same name?
  - Option: make `(name + degree_level)` a unique compound key in the schema

- Should we allow university admins to use existing program endpoints and **auto-create** a program template if none exists with the same title?
  - Problem: if a template with the same name but different `field_of_study`/`tags` already exists and takes over, the admin won't understand why their provided values were ignored

## Related Notes
- [[Tasks Manifest - Scholar Bee]]
