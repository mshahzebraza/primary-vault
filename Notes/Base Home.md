---
type: "[[Documentation]]"
categories:
  - "[[Documentation]]"
tags:
  - hub
  - navigation
original_path: Notes/Base Home.md
base: NotesRoot
---

# Base Home

Start here for **Bases** navigation. Canonical rules and property schema: [[Vault System Plan]]. Legacy field notes: [[Templates/Bases/Metadata contract]].

## Primary Bases (use these first)

Open from **Command palette → Bases: Open bases** (or embed links below).

| Base | Use for |
|------|---------|
| [[Templates/Bases/Tasks\|Tasks]] | Task, bug, and R&D notes — tabs by status, org, project |
| [[Templates/Bases/Meetings\|Meetings]] | Meeting notes; **By Task** groups by `related-tasks` |
| [[Templates/Bases/HQ\|HQ]] | Work overview by org and project; TechLearning; tag browser |
| [[Templates/Bases/Related Meetings\|Related Meetings]] | Embed in **task** notes — meetings that linked this task |
| [[Templates/Bases/Related Tasks\|Related Tasks]] | Embed in **meeting** notes — tasks from `related-tasks` |

## Legacy Bases (until `base` / `path_area` migration is finished)

| Base | Use for |
|------|---------|
| [[Templates/Bases/NotesByBase\|NotesByBase]] | All `Notes/` — filter by legacy **`base`** |
| [[Templates/Bases/WorkByOrganization\|WorkByOrganization]] | **`base == Work`** by **`organization`** |
| [[Templates/Bases/ByPathArea\|ByPathArea]] | Filter by **`path_area`** |
| [[Templates/Bases/Projects\|Projects]] | **Deprecated** — `[[Projects]]` category removed; use **`projects`** property + HQ / Tasks bases |

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
python3 scripts/category_cleanup.py --dry-run   # Phase 4 — already applied once
```

Phase 5 (remove `base`, `path_area`, `original_path`) when you are ready:

```bash
python3 scripts/vault_metadata.py remove-legacy --dry-run
```
