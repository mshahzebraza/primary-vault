---
type: "[[Documentation]]"
categories:
  - "[[Documentation]]"
  - "[[Work]]"
tags:
  - vault-system
  - plan
  - evergreen
date: 2026-04-05
status: active
organization:
  - "[[Personal]]"
---

# Vault System Plan

This document is the canonical reference for how this vault is structured, maintained, and navigated. It replaces all prior planning documents and Cursor plan files. When in doubt about how to create or organise a note, consult this file first.

---

## 1. Core Philosophy

**Three rules that prevent the system from collapsing under its own weight:**

1. **Metadata is filled once at creation, not maintained.** Status updates are two clicks (dropdown in Properties panel). Everything else stays fixed.
2. **Bases are the navigation layer. Folders and manifests are not.** Never manually maintain a list of tasks somewhere. If a Base doesn't surface it, the metadata is wrong — fix the metadata.
3. **When in doubt, write first, file later.** A note with incomplete metadata is infinitely better than a note not taken. The migration script can backfill metadata in bulk.

---

## 2. The Canonical Property Schema

Every note in `Notes/` should carry the applicable subset of these properties. Do not add properties outside this list.


### 2.1 Property Reference Table

| Property        | Type              | Allowed Values                                                                                                      | Required for         | Notes                                                              |
| --------------- | ----------------- | ------------------------------------------------------------------------------------------------------------------- | -------------------- | ------------------------------------------------------------------ |
| `type`          | wikilink          | `[[Task]]` `[[Bug]]` `[[Meeting]]` `[[RnD]]` `[[Documentation]]` `[[Journal]]` `[[Reference]]`                      | All notes            | Single value. Drives Base filtering.                               |
| `organization`  | wikilink          | `[[aiquery.io]]` `[[scholarbee]]` `[[Freelance]]`                                                                   | Work notes           | Single value.                                                      |
| `projects`      | list of wikilinks | `[[aq-client]]` `[[aq-infrastructure]]` `[[sb-backend]]` `[[sb-frontend-student]]` `[[sb-ops-scripts]]` `[[other]]` | Work notes           | **Multi-value list.** Omit for cross-project or non-project notes. |
| `categories`    | list of wikilinks | See §4                                                                                                              | All notes            | Multi-value. Drives Base filtering.                                |
| `status`        | text              | `active` `blocked` `backlog` `done` `open`                                                                          | Task, Bug notes      |                                                                    |
| `priority`      | text              | `P0` `P1` `P2` `P3`                                                                                                 | Task, Bug notes      | P0 = highest.                                                      |
| `date`          | date              | ISO 8601                                                                                                            | Meeting, Daily notes |                                                                    |
| `tags`          | tags              | See §5                                                                                                              | Optional for all     | Plain text, not wikilinks.                                         |
| `related-tasks` | list of wikilinks | `[[TaskNote]]`                                                                                                      | Meeting notes        | Powers meeting↔task relationship in Bases.                         |
| `parent-task`   | wikilink          | `[[ParentTask]]`                                                                                                    | Sub-task notes       | Optional. Creates task hierarchy.                                  |

### 2.2 Legacy fields (removed)

`base`, `path_area`, and `original_path` were **removed** from all notes in Phase 5. Navigation uses `type`, `categories`, `organization`, and `projects` only. Do not add these keys back to new notes.

### 2.3 Properties to Normalise Now

These are inconsistent names currently in the vault for the same concept:

| Current inconsistent names          | Canonical name                |
| ----------------------------------- | ----------------------------- |
| `company`, `organization`           | `organization` only           |
| `related`, `tasks`, `related-tasks` | `related-tasks` only          |
| `created`, `created_at`, `date`     | `date` only                   |
| `project` (single)                  | `projects` (list)             |
| `type: task` (plain text)           | `type: "[[Task]]"` (wikilink) |


---

## 3. The Three Primary Bases

Open these from `Base Home` or via the Command Palette (`Bases: Open bases`).

### 3.1 Tasks Base (`Tasks.base`)

**Purpose:** Replaces the manual task manifests as the source of truth for what is in flight.

**Filters:** Notes where `type` contains `[[Task]]`, `[[Bug]]`, or `[[RnD]]`, scoped to `Notes/`.

**Views (tabs):**

| Tab | Filter | Columns                                             | Sort |
| ---------- | ------------------------------------ | --------------------------------------------------- | ---------------------- |
| Active | `status: active` | name, organization, projects, priority, parent-task | priority ASC, name ASC |
| Blocked | `status: blocked` | name, organization, projects, priority              | priority ASC |
| Backlog | `status: backlog` | name, organization, projects, priority              | priority ASC |
| Done | `status: done` | name, organization, date modified                   | mtime DESC |
| aiquery.io | `organization` contains `aiquery.io` | name, projects, status, priority                    | status ASC, name ASC |
| scholarbee | `organization` contains `scholarbee` | name, projects, status, priority                    | status ASC, name ASC |
| By Project | grouped by `projects` | name, organization, status, priority                | — |

**What the manifests become:** Sprint narrative notes. They stop being edited as task lists. They become a pinned short-form summary of the current focus written in prose, linking to relevant task notes. The Tasks Base replaces their functional role.

### 3.2 Meetings Base (`Meetings.base`)

**Purpose:** All meeting notes, queryable by org, date, and linked task.

**Filters:** Notes where `categories` contains `[[Meetings]]`, scoped to `Notes/`.

**Views (tabs):**

| Tab | Filter | Columns | Sort |
|---|---|---|---|
| All Meetings | — | name, date, organization, related-tasks | date DESC |
| aiquery.io | `organization` contains `aiquery.io` | name, date, related-tasks | date DESC |
| scholarbee | `organization` contains `scholarbee` | name, date, related-tasks | date DESC |
| By Task | grouped by `related-tasks` | name, date, organization | date ASC |

The **By Task** tab is the answer to "show me every meeting that discussed X task." Click a task wikilink in the `related-tasks` column and the view filters to just that task's meetings.

### 3.3 HQ Base (`HQ.base`)

**Purpose:** Landing pad. Overview of all work notes by organisation and project. Supersedes the old `NotesByBase` / `ByPathArea` / `Projects` bases (removed in Phase 5); `WorkByOrganization.base` remains as an org-sliced view using `categories` + `organization`.

**Filters:** All notes in `Notes/`, excluding Templates.

**Views (tabs):**

| Tab | Filter | Columns | Group by |
|---|---|---|---|
| Overview | `categories` contains `[[Work]]` | name, type, organization, projects, status | organization |
| aiquery.io | organization = aiquery.io | name, type, projects, status | projects |
| scholarbee | organization = scholarbee | name, type, projects, status | projects |
| TechLearning | categories contains `[[TechLearning]]` | name, tags, date modified | — |
| Documentation | categories contains `[[Documentation]]` | name, type, organization, tags | — |
| Personal | categories contains `[[Personal]]` | name, type, tags, date modified | — |
| Tags Browser | all notes (grouped by tags) | name, type, tags | tags |


---

## 4. Categories — What They Are, What Stays, What Goes

### 4.1 The Rule

**Categories** are structural routing keys. They determine where a note appears in a Base. They are wikilinks to hub notes in `Categories/`. The list is small, stable, and intentional. You almost never add new ones. If you're unsure whether something should be a category, it should be a tag.

**Categories answer the question: "What kind of thing is this and where does it belong?"**

### 4.2 Categories to Keep

These are the canonical categories going forward. All other `Categories/` hub notes should be deleted.

| Category | Hub note | What belongs here |
|---|---|---|
| `[[Work]]` | `Categories/Work.md` | All work notes (aiquery.io, scholarbee, Freelance) |
| `[[aiquery.io]]` | `Categories/aiquery.io.md` | All aiquery.io notes |
| `[[scholarbee]]` | `Categories/scholarbee.md` | All scholarbee notes |
| `[[Freelance]]` | `Categories/Freelance.md` | All freelance project notes |
| `[[Meetings]]` | `Categories/Meetings.md` | All meeting notes |
| `[[Tasks]]` | `Categories/Tasks.md` | All task and bug notes |
| `[[Documentation]]` | `Categories/Docs.md` | Docs, reference, and how-to notes |
| `[[TechLearning]]` | `Categories/TechLearning.md` | All tech learning and self-study notes |
| `[[Personal]]` | `Categories/Personal.md` | Personal journal, life notes |
| `[[Journal]]` | `Categories/Journal.md` | Daily notes and journal entries |
| `[[Others & Misc]]` | `Categories/Others & Misc.md` | Uncategorized or misc notes that do not fit other hubs |

### 4.3 Categories to Delete

These are over-granular sub-topic hubs that belong as **tags**, not categories. Their notes will be updated to use tags instead, then these hub files can be removed.

| Delete | Replace with tag |
|---|---|
| `Categories/OpenClaw.md` | tag: `open-claw` |
| `Categories/OSSU notes.md` | tag: `ossu` |
| `Categories/linux-pc-setup.md` | tag: `linux-pc-setup` |
| `Categories/Solar System.md` | tag: `solar-system` |
| `Categories/Misc.md` | tag: `misc` or just remove (no replacement needed) |
| `Categories/NotesRoot.md` | Legacy migration artifact — delete |
| `Categories/Attachments.md` | Legacy migration artifact — delete |
| `Categories/R&D.md` | Replaced by `type: [[RnD]]` — delete |
| `Categories/People.md` | Not actively used — delete |
| `Categories/Evergreen.md` | Not actively used — delete |
| `Categories/Clippings.md` | Not actively used — delete |
| `Categories/Projects.md` | Replaced by `projects` property — delete |
| `Categories/Resources.md` | Replaced by `type: [[Reference]]` — delete |

**Process for deleting a category hub:**
1. Find all notes that have `"[[CategoryName]]"` in their `categories` field (use omnisearch or a Base filter)
2. Remove the category wikilink from those notes
3. Add the replacement tag if applicable
4. Delete the `Categories/CategoryName.md` hub file
5. Run `sync-categories` script if needed to clean up


---

## 5. Tags — What They Are and How They Work

### 5.1 The Rule

**Tags** are topical labels. They describe *what the note is about*, not where it belongs. They are plain text (not wikilinks). They are applied loosely — you don't need a complete taxonomy before you start.

**Tags answer the question: "What subject matter does this note touch?"**

### 5.2 Current Canonical Tag Vocabulary

Use these consistently. Avoid variations (e.g. use `backend` not `back-end`).

**Tech topics:** `backend` `frontend` `AI` `automation` `devops` `search-engines` `databases`

**Personal setup topics:** `linux-pc-setup` `open-claw` `dotfiles` `ossu` `solar-system`

**Domain topics:** `legal` `resources` `cs-notes`

**Work type labels** (used when `type` alone isn't specific enough): `feature` `script` `checklist` `migration` `refactor` `bug-fix`

### 5.3 The Promotion Flow (Tag → Category)

If you notice a tag appearing on 10 or more notes and you find yourself wanting to navigate *to all notes on that topic*, it's ready for promotion.

**Steps to promote a tag to a category:**
1. Decide on a canonical name (e.g. `open-claw` → `[[OpenClaw]]`)
2. Create `Categories/OpenClaw.md` as a hub note
3. Run a find-and-replace across `Notes/` to add `"[[OpenClaw]]"` to `categories` on all notes that have the `open-claw` tag
4. Optionally remove the tag from those notes (it becomes redundant)
5. Add the new category to the **Keep** table in §4.2 of this document
6. Add a view tab for it in the HQ Base if warranted

### 5.4 Tag Browser

The **Tags Browser** tab in the HQ Base shows all notes grouped by their tags. This is the canonical way to browse what exists across a topic area. There is no separate "tags note" — the Base view serves this function.


---

## 6. Templates

Every note type has a template. Access via Command Palette: `Templates: Insert template`.

### 6.1 Template Reference

| Template file | Use when | Key properties it sets |
|---|---|---|
| `Meeting Template.md` | Any meeting, sync, or client call | `type: [[Meeting]]`, `categories: [[Meetings]]`, `date`, `organization`, `related-tasks` |
| `Task Note Template.md` | Any standalone task or feature note | `type: [[Task]]`, `organization`, `projects`, `status: backlog`, `priority` |
| `Bug Template.md` | Any bug report | `type: [[Bug]]`, `organization`, `projects`, `status: open`, `priority` |
| `RnD Template.md` | Research, architecture exploration, or design | `type: [[RnD]]`, `organization`, `projects`, `status: draft` |
| `Daily Note Template.md` | Auto-created daily note | `type: [[Journal]]`, `categories: [[Journal]]`, `date` |
| `Journal Template.md` | Personal journal entry | `type: [[Journal]]`, `categories: [[Personal]]`, `date` |
| `Project Overview Template.md` | New client/project onboarding | `type: [[Documentation]]`, `organization`, `projects` |

### 6.2 Template Usage Rules

- **Always** use a template when creating a new note. Don't start with a blank file.
- **Fill `organization` and `projects` first** — these drive which Base tabs surface the note.
- **`status` defaults to `backlog`** for tasks. Change to `active` when you start working on it.
- **`related-tasks` on meeting notes** — fill this before closing the meeting note. It's the one field that enables the whole meeting↔task linking system.
- If you create a note without a template, add frontmatter manually before closing it.

### 6.3 Mini-Bases Inside Notes (Task ↔ Meeting Cross-Reference)

Two embedded Bases are designed to be placed inside note bodies:

**Inside any Task note** — shows all meetings that referenced this task:
```
![[Templates/Bases/Related Meetings.base]]
```
This works because `Related Meetings.base` filters on `related-tasks` containing `this` (the current note's filename).

**Inside any Meeting note** — shows all task notes linked from this meeting:
```
![[Templates/Bases/Related Tasks.base]]
```
This works because `Related Tasks.base` shows all notes whose filename appears in the current note's `related-tasks` list.

Both base files need to be created as part of the implementation. Once created, add the embed to the Meeting and Task Note templates so every new note gets it automatically.


---

## 7. The Seven Workflows

### Workflow 1 — Taking Meeting Notes

**Trigger:** You're about to join or have just finished a meeting.

**Steps:**
1. Create a new note from `Meeting Template.md`
2. Name it: `YYYYMMDDHHII - Topic.md` (e.g. `202604151430 - Dashboard sync.md`)
3. Fill `organization`, `date`, `attendees` in the frontmatter
4. During the meeting: write bullets in `## Discussion`
5. After the meeting: move confirmed decisions to `## Decisions Made`, open items to `## Action Items`
6. **Critical step:** fill `related-tasks` with wikilinks to every task this meeting touched. If a task note doesn't exist yet, create a stub file for it now (title + frontmatter only) and link it.
7. Done. The Meetings Base and the Related Meetings embed inside each linked task will automatically reflect this meeting.

**Time cost:** 2 minutes during meeting setup + 3 minutes filing after.

---

### Workflow 2 — Creating a Task Independently

**Trigger:** You identify a piece of work outside of a meeting.

**Steps:**
1. Create a new note from `Task Note Template.md`
2. Name it descriptively: `Feature - Export CSV.md` or `BUG - Dropdown closes on first click.md`
3. Fill `organization`, `projects`, `status: backlog`, `priority`
4. Write `## Overview` — one paragraph describing what and why
5. Write initial `## Current Tasks` checkboxes
6. The note will appear in the Tasks Base → Backlog tab automatically

**You do not need to add it to a manifest.** The Tasks Base surfaces it.

---

### Workflow 3 — Recording Task Updates and Finding Action Items

**Trigger:** Something changes on a task — new requirements from a meeting, a blocker resolved, partial completion.

**Steps:**
1. Open the task note
2. Change `status` in the Properties panel if the state changed (two clicks)
3. Add a `### YYYY-MM-DD` subsection at the top of the note body with what changed. Most recent update is always visible first.
4. Tick off completed checkboxes in `## Current Tasks`
5. New action items go as new checkboxes in `## Current Tasks`

**To find current action items:** Open the task note. All unticked checkboxes in `## Current Tasks` are the outstanding items. The dated subsections above give the full history.

---

### Workflow 4 — Recording R&D

**Trigger:** You need to explore an architecture option, evaluate a library, or research an approach before implementing.

**Steps:**
1. Create a note from `RnD Template.md`
2. Set `type: [[RnD]]`, `organization`, `projects`, `status: draft`
3. Write Overview, Requirements, Implementation Phases, and Open Questions sections
4. When the R&D produces a decision that affects a task: open the relevant task note and add this R&D note to `related-tasks` on it (or link it in the task body under a `## Related R&D` section)

---

### Workflow 5 — Vault Maintenance, Rules, and Internal Documentation

**Trigger:** You need to document how something in the vault works, update a plan, or write a rule.

**Steps:**
1. Create a note from any template or blank, depending on the format needed
2. Set `type: [[Documentation]]`, `categories: [[Documentation]]`
3. No `organization` field — these are vault-level, not project-level
4. Store in `Notes/` root with a clear descriptive name

This document itself (`Vault System Plan.md`) follows this workflow.

---

### Workflow 6 — Personal Setup Documentation (OpenClaw, Dotfiles, Solar, etc.)

**Trigger:** You're documenting a personal tech setup, home project, or reference guide.

**Steps:**
1. Create a note (no specific template needed for most of these)
2. Set `type: [[Reference]]` or `[[Documentation]]`
3. Set relevant tag(s): `open-claw`, `dotfiles`, `solar-system`, `linux-pc-setup`
4. Set `categories: [[TechLearning]]` for tech notes, `categories: [[Personal]]` for life/home notes
5. No `organization` field

These appear in the HQ Base → TechLearning tab and the Tags Browser.

---

### Workflow 7 — Freelance Project Updates

**Trigger:** A freelance client's timeline changes, payment is received, or requirements are submitted.

**Steps:**
1. Open the existing project note (e.g. `Aurangzeb - Website.md`)
2. Add a `### YYYY-MM-DD update` entry at the top of the note body with what changed
3. Update any status fields in the frontmatter if applicable
4. For a new client/project, create from `Project Overview Template.md` with `organization: [[Freelance]]`

These appear in HQ Base → Overview → Freelance group.


---

## 8. Daily Notes

Daily notes are **hubs, not task trackers.** They are not filled manually.

**Location:** `Daily/` folder (not `Notes/`)
**Auto-creation:** Obsidian's core Daily Notes plugin creates them automatically. Set it up at: Settings → Daily Notes → New file location: `Daily/`, Template: `Templates/Daily Note Template.md`
**Naming:** `YYYY-MM-DD.md` (e.g. `2026-04-15.md`)

**What goes in a daily note:**
- A free-form `## Scratch` section for any quick thought you want to capture
- Nothing else is typed manually

**How context accumulates automatically:**
- Meeting notes taken today have `date: 2026-04-15` in their frontmatter — the Daily Base can surface all notes from that date
- The daily note itself serves as the navigational anchor for the day if needed

**What the daily note is NOT:**
- Not a task tracker (Tasks Base handles this)
- Not a meeting log (Meetings Base handles this)
- Not a daily standup note (create a meeting note for that)

---

## 9. Navigation Quick Reference

| I want to see... | Go to |
|---|---|
| All active tasks | Tasks Base → Active tab |
| Active tasks for one project | Tasks Base → aiquery.io or scholarbee tab |
| All meetings | Meetings Base → All Meetings tab |
| All meetings about a specific task | Meetings Base → By Task tab |
| Everything for aiquery.io | HQ Base → aiquery.io tab |
| All notes with a specific tag | HQ Base → Tags Browser tab |
| A specific note | Quick Switcher (Ctrl/Cmd + O) or Omnisearch |
| The current sprint focus | [[Tasks Manifest - Ai Query]] or [[Tasks Manifest - Scholar Bee]] (narrative notes) |

---

## 10. Implementation Phases

### Phase 1 — Schema and Templates (do first, ~1 hour)
- [x] Update all templates: add `type`, `projects` (plural list), `related-tasks`
- [x] Remove inconsistent fields (`company`, `created_at`, `related`, `tasks`) from templates
- [x] Update `types.json` to reflect the canonical property list

### Phase 2 — Build Tasks Base and upgrade Meetings Base (~1 hour)
- [x] Create `Templates/Bases/Tasks.base` with all views per §3.1
- [x] Upgrade `Templates/Bases/Meetings.base` to add `related-tasks` column and By Task view
- [x] Create `Templates/Bases/HQ.base` to replace WorkByOrganization/NotesByBase/ByPathArea
- [x] Create `Templates/Bases/Related Meetings.base` (mini-base for task notes)
- [x] Create `Templates/Bases/Related Tasks.base` (mini-base for meeting notes)

### Phase 3 — Bulk metadata update on existing notes (~30 min, script)
- [x] Run script to normalise `company` → `organization` on all remaining notes
- [x] Run script to normalise `related`/`tasks` → `related-tasks` on meeting notes
- [x] Run script to seed `type`, `projects`, `priority`, `status` on task/bug notes missing them
- [x] Validate with `audit-metadata` script command

### Phase 4 — Category cleanup (~30 min)
- [x] Delete the 13 categories listed in §4.3
- [x] Update affected notes to use tags instead
- [x] Verify remaining 10 categories in §4.2 have correct notes pointing to them

### Phase 5 — Remove legacy fields (do last, after Phase 3 is confirmed stable)
- [x] Script pass to remove `base`, `path_area`, `original_path` from all notes
- [x] Update all Bases to not reference these fields
- [x] Delete `NotesByBase.base`, `ByPathArea.base`, and `Projects.base` (replaced by HQ / `projects` property)

---

## 11. What NOT to Do

- **Do not add new categories** without checking §4.2 first. If it's not on the keep list, it's a tag.
- **Do not maintain manifest bullet lists.** Change the task note's `status` field instead.
- **Do not add more than 4–5 properties to a note.** If you need more, the metadata schema has expanded beyond what Bases can usefully filter on.
- **Do not use `base`, `path_area`, or `original_path`.** They were removed in Phase 5; use `type`, `categories`, `organization`, and `projects`.
- **Do not create category hub notes for repos or codebases** (like `[[aq-client]]`). Those belong in the `projects` property, not as category hubs. Project-level navigation is handled by the `projects` column in the Tasks Base.

---

*Last updated: 2026-04-05. Phases 1–5 complete. This is a living document — update it when the system changes.*
