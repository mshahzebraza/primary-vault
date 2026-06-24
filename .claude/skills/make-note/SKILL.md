---
name: make-note
description: Create a structured, well-formed note in this Obsidian vault. Use whenever the user says "save this as a note", "make a note", "create a task/meeting/bug/journal/reference note", "capture this", "log this", or hands over content to file in the vault. Enforces the filename convention, metadata-contract frontmatter, the right template, and post-creation steps (manifest embedding, meeting↔task links) so notes stay searchable and consistent instead of becoming dumps.
---

# make-note

Turn loose input into a properly-structured vault note. Never write a note free-form — always follow the steps below so frontmatter, filename, and placement stay consistent and searchable.

## 1. Pick the note type

Map the content to ONE primary type (frontmatter `type` is a wikilink):

| Type | Use when | Template |
|------|----------|----------|
| `[[Task]]` | actionable work item | `Templates/Task Note Template.md` |
| `[[Bug]]` | a defect to fix | `Templates/Bug Template.md` |
| `[[Meeting]]` | notes from a meeting | `Templates/Meeting Template.md` |
| `[[RnD]]` | research / exploration | `Templates/RnD Template.md` |
| `[[Documentation]]` | reference docs / how-to | `Templates/Documentation Template.md` |
| `[[Journal]]` | dated personal log | `Templates/Journal Template.md` |
| `[[Reference]]` | external resource / clipping | `Templates/Clipping Template.md` |

If unsure between two, ask the user. Don't guess on type — it drives every Base view.

## 2. Get the timestamp (always, before naming)

```bash
date +"%y%m%dT%H%M"   # e.g. 260624T2014
date +"%a"            # weekday, e.g. Tue
```

Filename: `YYMMDDTHHMM (Weekday) <Type> - <Title>.md`
Example: `260624T2014 (Tue) Task - Wire up auth refresh.md`
Save under `Notes/` (dailies go in `Daily/`, journals follow the Journal template's location).

## 3. Fill frontmatter from the metadata contract

Read `Templates/Bases/Metadata contract.md` for the authoritative schema. Rules:

- `type` — wikilink(s), multitext: `"[[Task]]"`
- `organization` — single org wikilink for **work** notes only: `"[[scholarbee]]"`, `"[[aiquery.io]]"`, `"[[Freelance]]"`. Omit/blank for personal notes.
- `categories` — quoted hub wikilinks: `"[[Work]]"`, `"[[Tasks]]"`, `"[[Meetings]]"`, `"[[Personal]]"`
- `status` — `backlog | active | blocked | done` (tasks/bugs)
- `priority` — `P1 | P2 | P3` (tasks/bugs)
- `date` — `YYYY-MM-DD` (use today's date)
- `tags` — plain string labels, NOT wikilinks
- Quote YAML list items: `- "[[Tasks]]"`
- NEVER add legacy keys: `base`, `path_area`, `original_path`, `org`, `client`

Copy the matching template's body structure (e.g. Task = `## Overview` → `## Current Tasks` checklist).

## 4. Post-creation steps (don't skip)

- **Task note** → embed its action items in the relevant manifest:
  - ScholarBee/AiQuery → `Notes/Tasks Manifest - Scholar Bee.md`
  - Personal → `Notes/Tasks Manifest - Personal.md`
  - Manifest section order: `## ▶️ In Progress` → `## 🟥 Pending` → `## ⚠️ Blocked` → `## ✅ Completed` → `## Ideas/Future Requirements` → `## Tech Debt`
- **Meeting note** → set `related-tasks` frontmatter linking to any task notes; push extracted action items into the relevant task note or manifest.

## 5. Confirm

Report the created filename (as a clickable link) and what manifest/links you updated.
