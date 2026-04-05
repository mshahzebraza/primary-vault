# Metadata contract (Bases + Properties)

Notes under `Notes/` use a small YAML set so **Bases** and **Properties** stay consistent. **Path-aware fields** (`base`, `organization`, `path_area`) come from the **canonical pre-flat path** via `scripts/path_map.json` when present, not only from today’s flat filename.

## Primary fields (navigation)

| Field | Type (see `.obsidian/types.json`) | What to put |
|--------|-----------------------------------|-------------|
| `original_path` | text | Vault-relative path where the note *logically* lived before flattening (POSIX). `inject` prefers `path_map.json` when the flat file maps to an old path. |
| `base` | text | Top bucket: `Work`, `TechLearning`, `Personal`, `Resources`, `NotesRoot`, `Attachments`, … |
| `organization` | text | **Single value** (not a list): employer / client / umbrella, as a wikilink string, e.g. `organization: "[[aiquery.io]]"`. |
| `path_area` | text | **Single value** (not a list): area slug from the old path, plain text — e.g. `Tasks`, `Docs`, `R&D` (use quotes if needed, e.g. `"R&D"`). Use `categories` for `[[Tasks]]`-style hub links. |

## Steph-style: `categories` (wikilinks)

| Field | Type | What to put |
|--------|------|-------------|
| `categories` | multitext | List of `[[Hub]]` links to notes in `Categories/`—e.g. `[[Work]]`, `[[aiquery.io]]`, `[[Tasks]]`, `[[Meetings]]`, `[[Projects]]`. |

**YAML:** Each list item must be **double-quoted**, e.g. `- "[[Meetings]]"`. Unquoted `[[...]]` is parsed by YAML as nested arrays, which breaks Obsidian Properties and shows warnings.

**Hub notes:** stubs live under `Categories/` so links resolve. Each hub note should embed a **Bases** view for quick navigation, e.g. `![[Templates/Bases/Meetings.base]]`, `![[Templates/Bases/WorkByOrganization.base#aiquery.io]]` (use `#ViewName` to open a specific tab). See notes under `Categories/`.

## Tags and status

| Field | Type | What to put |
|--------|------|-------------|
| `tags` | tags | Plural, shared vocabulary. |
| `status` | multitext | Where a note has a lifecycle (tasks, projects). |

## Repair commands (vault root)

```bash
python3 scripts/migrate_notes_flat.py inject
python3 scripts/migrate_notes_flat.py fix-meta
python3 scripts/migrate_notes_flat.py sync-categories
python3 scripts/migrate_notes_flat.py audit-metadata
```

**Artifacts:** `scripts/path_map.json`, `scripts/migration_manifest.json`.

## Types file

Obsidian reads property UI types from `.obsidian/types.json`. Human-readable “what to fill” text is this note.

## Projects vs meetings

- **`[[Meetings]]`** — meeting notes; filename containing `meeting` gets this category from `sync-categories` (heuristic).
- **`[[Projects]]`** — work tied to products/repos/apps; added for **Work** notes in **R&D** or **Docs** `path_area` (heuristic). Add more specific hubs under `Categories/` (e.g. product name) and link them in `categories` as needed.
