---
name: resolve-meeting
description: Process a rough meeting note into the vault. Use when the user says "resolve this meeting", "process my scrum notes", "sort out this meeting", "file these meeting notes", or hands over raw meeting/scrum notes to organize. Extracts action items, batches clarifying questions, summarizes its understanding, then on approval routes each item to the right feature doc or task manifest, links the meeting both ways, marks superseded instructions, and fixes frontmatter — so nothing stays stranded in the meeting note.
---

# resolve-meeting

Turn a rough meeting note into linked, findable work. Phases 1–3 are **read-only**; only phase 4 writes, and only after the user approves.

## 1. Intake
- Read the target note + its frontmatter.
- Establish org context: from `organization`, grep recent same-org meetings, feature docs, and the matching manifest (`Notes/Tasks Manifest - *.md`) so you can match items to existing work.

## 2. Understand
Extract every action item / discussion point. Classify each as one of:
`feature` · `task` · `decision` · `bug` · `question`.

## 3. Clarify — STOP for approval
Present in one message:
1. A short **summary of understanding** (what the meeting was about, the items found).
2. **All** clarifying questions, batched (ambiguities that change routing).
3. A **routing plan**: each item → its destination.

Then wait. Do not write until the user approves.

## 4. Execute (after approval)
Route each item to exactly one home:

| Class | Destination |
|-------|-------------|
| `feature` (substantial / multi-step) | Find the existing feature doc (grep title + wikilinks). Update the relevant section and add a `related-tasks` link. If none exists, create one via the **make-note** skill in Task shape, set `status` (`backlog`/`active`). |
| `task` (small / standalone) | The org manifest — correct section, linked to a related task note if one exists. |
| `decision` | The feature doc's `## Decisions` section. Mark any instruction it overrides as superseded (see convention). |
| `bug` | Existing bug note if present, else a manifest bug line under the right priority. |
| `question` | Manifest "Open Questions" / Unknowns, or hand back in the CONFIRM report — never drop silently. |

Then:
- Set `related-tasks` on the **meeting note** pointing at every doc you touched (link both ways).
- Run `python3 scripts/vault_metadata.py audit`, grep for the files you created/edited, and fix any flagged frontmatter (legal `status`: `backlog|active|blocked|done`; no template placeholders; `[[Work]]` not `[[Personal]]` for work meetings).

### Conventions
- **Superseded instruction:** above the old item add a collapsed callout — `> [!info]- Superseded by [[new note]]` — keeping history but closing the loose end.
- **Templates are a baseline, not a cage.** If an item does not fit the template's sections, **add or rename sections** in the task/feature note to match the need. Never force-fit or drop info.
- **Manifest section order:** `## ▶️ In Progress` → `## 🟥 Pending` → `## ⚠️ Blocked` → `## ✅ Completed` → `## Ideas/Future Requirements` → `## Tech Debt`.

## 5. Confirm
Report (as clickable links): notes created/updated, manifest sections changed, supersede markers added, and any items handed back to the user.
