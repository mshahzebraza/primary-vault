---
name: vault-audit
description: Read-only health report for the Obsidian vault. Use when the user says "audit my vault", "vault audit", "find loose ends", "what's drifting in my vault", "check my notes for problems", or wants to find stranded meeting items, metadata violations, broken links, or manifest rot. Reports findings only — never edits notes.
---

# vault-audit

Produce a findings report. **Never edit notes** — this skill only reads and reports. Group findings by area; cite each with the note filename (as a clickable link) and a one-line fix.

## Checks

1. **Metadata violations** — run `python3 scripts/vault_metadata.py audit` and surface its output (missing `type`, unreadable frontmatter, etc.). Add contract checks it misses: illegal `status` (not `backlog|active|blocked|done`), leftover template placeholders like `"{ date: YYYY-MM-DD }"`, work meetings tagged `[[Personal]]` instead of `[[Work]]`, legacy keys (`base`, `path_area`, `original_path`, `org`, `client`).

2. **Stranded meeting items** — for each `[[Meeting]]` note, check whether its Action Items are linked into a feature doc or a manifest. Flag meetings whose items appear nowhere else (the classic "captured then forgotten" case).

3. **Broken / orphaned links** — wikilinks and embeds (`![[note#section]]`) that point at a missing note or a heading that no longer exists.

4. **Manifest hygiene** — in `Notes/Tasks Manifest - *.md`: done `[x]` items left in active sections, large spec blobs pasted inline that should be their own note, and missing/!out-of-order canonical sections.

5. **Possible supersession** — the same feature/instruction marked done in one note and reopened later in another, with no superseded marker linking them.

## Output
A grouped report. For the AiQuery manifest specifically, flag it for restructuring to the canonical section order if it has drifted — but do not restructure it here. End with a short "top 3 to fix first" list.
