# Metadata contract (Bases + Properties)

Notes under `Notes/` follow the **canonical property schema** in [[Vault System Plan]] (§2). This file summarizes types and tooling.

## Primary fields

| Field | Type (`.obsidian/types.json`) | Notes |
|-------|-------------------------------|--------|
| `type` | multitext | Wikilinks: `[[Task]]`, `[[Bug]]`, `[[Meeting]]`, `[[RnD]]`, `[[Documentation]]`, `[[Journal]]`, `[[Reference]]` |
| `organization` | multitext | Single org wikilink for work notes, e.g. `"[[aiquery.io]]"` |
| `projects` | multitext | Multi-value; project hubs are **not** categories |
| `categories` | multitext | Quoted wikilinks to hub notes in `Categories/` |
| `status` / `priority` | text | Tasks, bugs (see plan §2.1) |
| `date` | date | Meetings, journals, dailies |
| `related-tasks` | multitext | Meeting ↔ task linking |
| `tags` | tags | Topical labels (not wikilinks) |

**YAML:** Quote list items: `- "[[Meetings]]"`.

## Legacy (removed)

`base`, `path_area`, and `original_path` were removed from notes in **Phase 5**. Navigation uses `type`, `categories`, `organization`, and `projects` instead. Do not reintroduce those keys.

## Scripts (vault root)

```bash
pip install -r scripts/requirements.txt
python3 scripts/vault_metadata.py normalize
python3 scripts/vault_metadata.py audit
python3 scripts/vault_metadata.py remove-legacy
python3 scripts/normalize_property_keys.py   # merge created→date, drop plugin keys, etc.
```

### `.obsidian/types.json`

Registered types are the **canonical** fields above plus: `aliases` (Obsidian), `attendees` (meetings), `author` / `source` / `url` / `published` / `topics` / `clipped` (clippings). The monthly template may still use `previous` / `next` in YAML; they are not registered in `types.json`. **Not** registered: plugin-only keys (`sticker`, `banner_y`), duplicate spellings (`Status`, `created` as a second date), `severity` (use `priority`), `client` / `org` / `twitter` (use `tags` + `organization`).

## Hub embeds

Category hub notes under `Categories/` embed **HQ**, **Tasks**, **Meetings**, or **WorkByOrganization** bases — see each hub file.
