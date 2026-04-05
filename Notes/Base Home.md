---
tags:
  - hub
  - navigation
original_path: Notes/Base Home.md
base: NotesRoot
categories:
  - "[[NotesRoot]]"
---

# Base Home

Start here for **navigation by base**, **organization**, **path area**, and **categories** (wikilinks). Full detail: [[Templates/Bases/Metadata contract]].

## Bases (tables and filters)

Open these in Obsidian (Bases plugin). Use **view tabs** inside each base for slices (Work, TechLearning, org, path area, meetings, projects).

| Base file | Use for |
|-----------|---------|
| [[Templates/Bases/NotesByBase|NotesByBase]] | Every note under `Notes/` — sort and filter by **`base`**. |
| [[Templates/Bases/WorkByOrganization|WorkByOrganization]] | **`base == Work`** — split by **`organization`** (aiquery.io, scholarbee, Freelance). |
| [[Templates/Bases/ByPathArea|ByPathArea]] | Filter by **`path_area`** (Tasks, Docs, R&D, …). |
| [[Templates/Bases/Meetings|Meetings]] | Notes with **`categories`** containing **`[[Meetings]]`**. |
| [[Templates/Bases/Projects|Projects]] | Notes with **`categories`** containing **`[[Projects]]`** (products/repos/apps under an org). |

Legacy bases for clippings/journal/dailies (optional): [[Templates/Bases/Clippings]], [[Templates/Bases/Journal]], [[Templates/Bases/Daily]].

## Category hubs (Steph-style)

- **`categories`** in YAML holds `[[Hub]]` links; hub notes live in the `Categories/` folder (e.g. [[Work]], [[TechLearning]], [[aiquery.io]], [[Tasks]], [[Meetings]], [[Projects]]).
- After path/metadata repair, run **`sync-categories`** so `categories` stays aligned with `base` / `organization` / `path_area` (see Metadata contract).

## Quick open (daily)

- **Command palette**: “Bases” to pick a base, or **Quick switcher** for a note by title.
- **Omnisearch** (plugin): search across the vault.
- **Tasks**: [[Tasks Manifest - Ai Query]], [[Tasks Manifest - Scholar Bee]].

## Bookmarks (one-time setup)

1. Right‑click **Base Home** in the file explorer → **Add bookmark**.
2. Bookmark your task manifests and daily note the same way.
3. **Settings → Hotkeys**: assign keys for **Bases: Open bases** and **Quick switcher** if you like.

## Metadata commands

From the vault root:

```bash
python3 scripts/migrate_notes_flat.py inject
python3 scripts/migrate_notes_flat.py fix-meta
python3 scripts/migrate_notes_flat.py sync-categories
python3 scripts/migrate_notes_flat.py audit-metadata
```
