# Resolve meetings & keep the vault from drifting

Visual source: `plan.mdx` (this dir). Serve: `npx @agent-native/core@latest plan local serve --dir plans/resolve-meeting --kind plan --open`.

## Context
Rough scrum items (sidebar redesign, "tags on query packs", liveshell tweaks) stay inside the meeting note and never reach a feature doc or manifest — invisible to Bases, unfindable later. Plus metadata drift (unfilled `date` placeholders, illegal `status: completed`, work meetings tagged `[[Personal]]`, AiQuery manifest typed `[[Documentation]]` and turning into a dump). Adds two skills; existing-drift cleanup deferred.

Settled: two skills; new feature docs reuse the Task shape; flow = summarize → batch questions → approve once → execute.

## Skill 1 — `resolve-meeting` (`.claude/skills/resolve-meeting/SKILL.md`)
5 phases, one approval gate; 1–3 read-only.
1. Intake — read note + frontmatter; grep recent same-org meetings/feature docs.
2. Understand — extract items; classify feature | task | decision | bug | question.
3. Clarify — summary + ALL questions + routing plan; STOP for one approval.
4. Execute — route each item to one home (feature doc update/create + `related-tasks` link / manifest section / decision + supersede marker); set meeting `related-tasks` both ways; run `vault_metadata.py audit`, fix frontmatter.
5. Confirm — report links, manifest changes, items handed back.

**Templates are a baseline, not a cage:** when an item does not fit the template sections, add or rename sections in the task/feature note rather than dropping info or force-fitting.

## Skill 2 — `vault-audit` (`.claude/skills/vault-audit/SKILL.md`)
Read-only report: stranded meeting items, metadata violations (wraps `vault_metadata.py audit`), broken/orphaned links + embeds, manifest hygiene, possible supersession.

## Reuse
`make-note` skill, `scripts/vault_metadata.py`, `Templates/`, both `Notes/Tasks Manifest - *.md`.

## Open questions (answer in the visual plan form)
1. Superseded marker: collapsed callout+link (rec) / strikethrough / archive section.
2. Decisions home: feature-doc Decisions (rec) / dedicated log / manifest.
3. AiQuery manifest restructure: vault-audit flags it (rec) / gradual normalize / leave.

## Non-goals
One-time drift cleanup; Bases/Categories changes; new Feature template; bulk edits during build.

## Verification
1. Dry-run `/resolve-meeting` on 260623 scrum — extracts items, STOPS at summary.
2. `vault_metadata.py audit` clean for new/updated docs.
3. Meeting gains `related-tasks`; manifest gains routed items in right sections.
4. `/vault-audit` reports known drift without editing.
5. "resolve this scrum" (no slash) auto-fires the skill.
