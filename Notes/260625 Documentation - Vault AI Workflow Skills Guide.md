---
type: "[[Documentation]]"
categories:
  - "[[Personal]]"
  - "[[TechLearning]]"
tags:
  - ai-workflow
  - obsidian
  - claude-code
  - skills
date: 2026-06-25
status: active
---

## Overview

This vault uses a set of Claude Code skills to automate recurring knowledge management workflows. The skills live in `.claude/skills/` and are triggered by natural language phrases during a Claude Code session. Together they keep the vault's metadata accurate, meeting notes actionable, and task notes honest about what's truly done vs. what still has polish left.

---

## Skills

### `vault-audit`

**Trigger:** `/vault-audit` or "run vault audit"

Read-only drift scanner. Produces a report of:
- Stranded meeting notes (not linked to any task or manifest)
- Metadata violations (missing `type`, wrong `status` values, unfilled template placeholders)
- Broken wikilinks and embeds
- Manifest hygiene issues (stale embeds, orphaned items)
- Possible supersession candidates

Run before any batch cleanup session to get a prioritised fix list. Output is read-only — no writes happen during audit.

---

### `resolve-meeting`

**Trigger:** `/resolve-meeting <filename>` or "resolve meeting <name>"

5-phase pipeline for turning a rough meeting note into linked, findable work:

| Phase | Action |
|-------|--------|
| 1. Intake | Read the meeting note + org manifest + recent related feature docs |
| 2. Understand | Classify each item as `feature`, `task`, `decision`, `bug`, or `question` |
| 3. Clarify | Present routing plan + all questions — **STOP and wait for approval** |
| 4. Execute | Route items to feature docs / manifests, fix frontmatter, link both ways |
| 5. Confirm | Report every file touched with clickable links |

**Routing table:**

| Class | Destination |
|-------|-------------|
| `feature` | Existing feature doc (or new Task note via make-note), add `related-tasks` |
| `task` | Org manifest — correct section |
| `decision` | Feature doc's `## Decisions` section; supersede old instructions with a callout |
| `bug` | Existing bug note or manifest bug line |
| `question` | Manifest "Open Questions" or handed back in CONFIRM — never dropped silently |

After routing, `related-tasks` is set on the meeting note and `python3 scripts/vault_metadata.py audit` is run on touched files to catch any metadata drift.

**Superseded instruction convention:**
```
> [!info]- Superseded by [[new note]]
> old instruction text
```

---

### `sync-enhancements`

**Trigger:** `/sync-enhancements` or "sync enhancements" or "update enhancement flags"

Reads every `[[Task]]`, `[[Bug]]`, and `[[RnD]]` note. For each note that has a `## Enhancements` section, counts open `[ ]` items and writes `has-enhancements: true/false` to the frontmatter. Notes without a `## Enhancements` section are skipped entirely — the field is never added to them.

Produces a report before writing: what will change, what's already in sync, what's being skipped.

After a sync, the **Enhancement Backlog** base (`Templates/Bases/Enhancement Backlog.base`) shows every `done` note with open enhancements, sortable by priority and date.

---

## Enhancement Lifecycle

### Status values

| Value | Meaning |
|-------|---------|
| `backlog` | Not started |
| `active` | Being worked on |
| `blocked` | Waiting on external dependency |
| `done` | All items in `## Current Tasks` complete; `## Enhancements` may still be open |
| `closed` | Fully retired — done with no follow-up, or explicitly cancelled |

### The `has-enhancements` flag

A checkbox frontmatter field (`true` / `false`). Set by `sync-enhancements` or manually. The Enhancement Backlog base queries `status == "done" AND has-enhancements == true`, making polish work visible without cluttering active views.

### Task note structure

```md
## Current Tasks
- [ ] Required item A
- [ ] Required item B

## Enhancements
> Optional improvements — open items here do not block `status: done`.
- [ ] Nice-to-have X
- [ ] Nice-to-have Y
```

---

## Manifest Embed Convention

- **While tasks are open:** embed the task note section in the manifest with `![[note#section]]`
- **Once all required tasks are done:** replace embed with `[x] [[note]]` in `## ✅ Completed`
- **No ad-hoc one-liners in Completed:** only dedicated-note links stay; quick fixes captured in meeting notes don't need manifest entries

---

## Filename Convention

All time-stamped notes use `YYMMDD <Type> - <Title>.md`.

- Example: `260625 Documentation - Vault AI Workflow Skills Guide.md`
- Full timestamp (`YYYY-MM-DD`) goes in `date:` frontmatter only — not in the filename
- Use `date +"%y%m%d"` to get the prefix before creating any note

68 notes were bulk-renamed on 2026-06-24 to drop the old `YYMMDDTHHMM (Weekday)` format.

---

## Scripts

```bash
# Audit vault metadata
python3 scripts/vault_metadata.py audit

# Normalize property keys (merge created→date, drop plugin keys)
python3 scripts/normalize_property_keys.py

# Bulk-set missing type fields
python3 scripts/vault_metadata.py normalize
```

Scripts live in `scripts/` at the vault root.
