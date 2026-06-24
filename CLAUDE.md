# Obsidian Vault — AI Agent Instructions

This is a personal second-brain Obsidian vault. All notes live under `Notes/`, templates under `Templates/`, category hubs under `Categories/`, and database views under `Templates/Bases/`.

## Organisations

Three canonical work orgs — always use wikilink syntax:
- `"[[scholarbee]]"` — ScholarBee backend work
- `"[[aiquery.io]]"` — AiQuery product work
- `"[[Freelance]]"` — freelance engagements

## Note filename convention

All time-stamped notes use `YYMMDD <Type> - <Title>.md`.
Examples: `260507 Task - ...`, `260423 Meeting - ...`

Use `date +"%y%m%d"` to get the current date before creating any note.
The full timestamp goes in the `date` frontmatter field only — not in the filename.

## Metadata contract

Every note under `Notes/` must have frontmatter conforming to `Templates/Bases/Metadata contract.md`. Key rules:
- `type` — multitext wikilink: `[[Task]]`, `[[Bug]]`, `[[Meeting]]`, `[[RnD]]`, `[[Documentation]]`, `[[Journal]]`, `[[Reference]]`
- `organization` — single org wikilink (work notes only)
- `categories` — quoted wikilinks e.g. `"[[Work]]"`, `"[[Tasks]]"`, `"[[Meetings]]"`, `"[[Personal]]"`
- `status` — `backlog | active | blocked | done | closed`. `done` = all required items in `## Current Tasks` complete; open `## Enhancements` items are expected and do not block it. `closed` = fully retired (done with no follow-up, or cancelled).
- `has-enhancements` — checkbox; `true` when `status: done` but `## Enhancements` still has open `[ ]` items. Synced by the `sync-enhancements` skill.
- `priority` — `P1 | P2 | P3`
- `date` — `YYYY-MM-DD`
- `tags` — plain string labels (not wikilinks)
- `read` — checkbox, **external-source notes only** (videos, articles, tutorials). Default `false` when creating from an external source. Set `true` only when user says they've already consumed it.
- `url` — source URL for external-source notes
- Do NOT use legacy fields: `base`, `path_area`, `original_path`, `org`, `client`

## Task notes

Template: `Templates/Task Note Template.md`
Sections: frontmatter → `## Overview` (one paragraph) → `## Current Tasks` (checklist) → optional embedded bases.
After creating a task note, always embed its action items in the relevant Tasks Manifest under `Notes/`.

### Task manifests
- ScholarBee: `Notes/Tasks Manifest - Scholar Bee.md`
- Personal: `Notes/Tasks Manifest - Personal.md`
- AiQuery tasks are inline in the ScholarBee manifest or get their own notes

Manifest sections order: `## ▶️ In Progress` → `## 🟥 Pending` → `## ⚠️ Blocked` → `## ✅ Completed` → `## Ideas/Future Requirements` → `## Tech Debt`

## Meeting notes

Template: `Templates/Meeting Template.md`
Sections: frontmatter → context → discussion → decisions → action items.
Link meetings to task notes via `related-tasks` frontmatter on the meeting note. Action items extracted from meetings go into the relevant task note or manifest.

## Daily notes

Live in `Daily/`. Filename format: `26-Mon-DD (Weekday) Daily Note.md` (e.g. `26-May-07 (Thu) Daily Note.md`).
Template: `Templates/Daily Note Template.md`
Sections: `## Scratch` then one `## <Org> Work` section per active organisation.

## Navigation entry points

- `Categories/Tasks.md` → Tasks.base (all active tasks)
- `Categories/Work.md` → HQ.base Overview + WorkByOrganization.base
- `Categories/Meetings.md` → Meetings.base
- `Categories/scholarbee.md` → ScholarBee work filtered view
- `Categories/aiquery.io.md` → AiQuery work filtered view
- `Notes/Tasks Manifest - Scholar Bee.md` — authoritative ScholarBee task board
- `Notes/Tasks Manifest - Personal.md` — personal setup tasks
