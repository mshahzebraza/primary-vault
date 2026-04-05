---
type: '[[Documentation]]'
categories:
- '[[Documentation]]'
tags:
- hub
- navigation
---

# Base Home

Start here for **Bases** navigation. Canonical rules and property schema: [[Vault System Plan]]. Technical reference: [[Templates/Bases/Metadata contract]].

## Primary Bases

Open from **Command palette → Bases: Open bases** (or embed links below).

| Base | Use for |
|------|---------|
| [[Templates/Bases/Tasks\|Tasks]] | Task, bug, and R&D notes — tabs by status, org, project |
| [[Templates/Bases/Meetings\|Meetings]] | Meeting notes; **By Task** groups by `related-tasks` |
| [[Templates/Bases/HQ\|HQ]] | Work (`[[Work]]`), org slices, TechLearning, Documentation, Personal, tags |
| [[Templates/Bases/WorkByOrganization\|WorkByOrganization]] | Work notes grouped by **`organization`** (same org tabs as before; uses `categories` + `organization`) |
| [[Templates/Bases/Related Meetings\|Related Meetings]] | Embed in **task** notes — meetings that linked this task |
| [[Templates/Bases/Related Tasks\|Related Tasks]] | Embed in **meeting** notes — tasks from `related-tasks` |

Optional: [[Templates/Bases/Clippings]], [[Templates/Bases/Journal]], [[Templates/Bases/Daily]].

## Category hubs

Hub notes live under `Categories/` (e.g. [[Work]], [[TechLearning]], [[aiquery.io]], [[Tasks]], [[Meetings]], [[Documentation]]). Use **`categories`** for structural routing; use **tags** for topics (see Vault System Plan §4–5).

## Quick open

- **Command palette**: Bases, Quick switcher, Templates: Insert template
- **Sprint narrative (not task lists)**: [[Tasks Manifest - Ai Query]], [[Tasks Manifest - Scholar Bee]]

## Metadata scripts (vault root)

```bash
python3 scripts/vault_metadata.py normalize
python3 scripts/vault_metadata.py audit
python3 scripts/vault_metadata.py remove-legacy --dry-run   # no-op if Phase 5 already applied
```
