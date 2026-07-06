# 📊 Graph Analysis Report

**Root:** `.`

## Summary

| Metric | Value |
|--------|-------|
| Nodes | 81 |
| Edges | 148 |
| Communities | 19 |
| Hyperedges | 0 |

### Confidence Breakdown

| Level | Count | Percentage |
|-------|-------|------------|
| EXTRACTED | 77 | 52.0% |
| INFERRED | 71 | 48.0% |
| AMBIGUOUS | 0 | 0.0% |

## 🌟 God Nodes (Most Connected)

| Node | Degree | Community |
|------|--------|-----------|
| migrate_notes_flat | 41 | 3 |
| vault_metadata | 18 | 0 |
| category_cleanup | 9 | 1 |
| normalize_property_keys | 9 | 2 |
| cmd_rewrite() | 9 | 6 |
| cmd_sync_categories() | 8 | 8 |
| main() | 8 | 9 |
| cmd_fix_meta() | 7 | 16 |
| split_first_frontmatter() | 7 | 4 |
| normalize_file() | 7 | 0 |

## 🔮 Surprising Connections

- **scripts_migrate_notes_flat_py_canonical_path_for_metadata** → **scripts_migrate_notes_flat_py_load_path_map_reverse** (calls)
- **scripts_migrate_notes_flat_py_metadata_for_inject** → **scripts_migrate_notes_flat_py_derive_metadata** (calls)
- **scripts_migrate_notes_flat_py_inject_lines_for_meta** → **scripts_migrate_notes_flat_py_yaml_quote** (calls)
- **scripts_migrate_notes_flat_py_derive_categories_wikilinks** → **scripts_migrate_notes_flat_py_org_wikilink** (calls)
- **scripts_migrate_notes_flat_py_cmd_sync_categories** → **scripts_migrate_notes_flat_py_metadata_for_inject** (calls)

## 🏘️ Communities

### Community 0 — remove_legacy_file() (19 nodes, cohesion: 0.19)

- vault_metadata
- audit_file()
- categories_str_list()
- cmd_audit()
- cmd_normalize()
- cmd_remove_legacy()
- dump_fm_body()
- has_category_meetings()
- has_category_tasks()
- argparse
- pathlib.Path
- re
- sys
- yaml
- load_fm_body()
- main()
- merge_wikilinks()
- normalize_file()
- remove_legacy_file()

### Community 1 — strip_category_name() (10 nodes, cohesion: 0.29)

- category_cleanup
- cleanup_note()
- argparse
- pathlib.Path
- re
- yaml
- load_fm()
- main()
- save_fm()
- strip_category_name()

### Community 2 — process_file() (10 nodes, cohesion: 0.27)

- normalize_property_keys
- dump_fm()
- argparse
- pathlib.Path
- re
- sys
- yaml
- is_bug_type()
- main()
- process_file()

### Community 3 — typing.Any (9 nodes, cohesion: 0.22)

- migrate_notes_flat
- argparse
- hashlib
- json
- os
- pathlib.Path
- re
- shutil
- typing.Any

### Community 4 — split_first_frontmatter() (3 nodes, cohesion: 0.67)

- cmd_audit_metadata()
- fm_has_key()
- split_first_frontmatter()

### Community 5 — yaml_quote() (3 nodes, cohesion: 0.67)

- categories_yaml_lines()
- restore_original_path_line()
- yaml_quote()

### Community 6 — rewrite_notes_paths() (3 nodes, cohesion: 0.67)

- cmd_rewrite()
- rewrite_markdown_links()
- rewrite_notes_paths()

### Community 7 — collect_notes_files() (2 nodes, cohesion: 1.00)

- cmd_inject()
- collect_notes_files()

### Community 8 — strip_categories_block() (2 nodes, cohesion: 1.00)

- cmd_sync_categories()
- strip_categories_block()

### Community 9 — main() (2 nodes, cohesion: 1.00)

- cmd_validate()
- main()

### Community 10 — load_path_map_reverse() (2 nodes, cohesion: 1.00)

- load_path_map()
- load_path_map_reverse()

### Community 11 — org_wikilink() (2 nodes, cohesion: 1.00)

- derive_metadata()
- org_wikilink()

### Community 12 — strip_wikilink() (2 nodes, cohesion: 1.00)

- derive_categories_wikilinks()
- strip_wikilink()

### Community 13 — rewrite_wikilinks() (2 nodes, cohesion: 1.00)

- resolve_link_target()
- rewrite_wikilinks()

### Community 14 — inject_lines_for_meta() (2 nodes, cohesion: 1.00)

- inject_frontmatter()
- inject_lines_for_meta()

### Community 15 — metadata_for_inject() (2 nodes, cohesion: 1.00)

- canonical_path_for_metadata()
- metadata_for_inject()

### Community 16 — join_frontmatter() (2 nodes, cohesion: 1.00)

- cmd_fix_meta()
- join_frontmatter()

### Community 17 — cmd_flatten() (2 nodes, cohesion: 1.00)

- build_path_map()
- cmd_flatten()

### Community 18 — collect_basename_index() (2 nodes, cohesion: 1.00)

- basename_no_ext()
- collect_basename_index()

## 🕳️ Knowledge Gaps

No isolated nodes.

**Thin communities** (< 3 nodes): 12 communities

## 💰 Token Cost

| File | Tokens |
|------|--------|
| input | 0 |
| output | 0 |
| **Total** | **0** |

## ❓ Suggested Questions

1. How does 'scripts_migrate_notes_flat_py_metadata_for_inject' relate to 5 different communities (typing.Any, collect_notes_files(), metadata_for_inject(), org_wikilink(), strip_categories_block())?
1. How does 'scripts_migrate_notes_flat_py_cmd_fix_meta' relate to 7 different communities (org_wikilink(), metadata_for_inject(), split_first_frontmatter(), join_frontmatter(), main(), typing.Any, inject_lines_for_meta())?
1. How does 'scripts_migrate_notes_flat_py_cmd_validate' relate to 3 different communities (split_first_frontmatter(), typing.Any, main())?
1. How does 'scripts_migrate_notes_flat_py_split_first_frontmatter' relate to 7 different communities (rewrite_notes_paths(), split_first_frontmatter(), strip_categories_block(), join_frontmatter(), inject_lines_for_meta(), typing.Any, main())?
1. How does 'scripts_migrate_notes_flat_py_rewrite_wikilinks' relate to 3 different communities (rewrite_wikilinks(), rewrite_notes_paths(), typing.Any)?
1. How does 'scripts_migrate_notes_flat_py_inject_frontmatter' relate to 5 different communities (inject_lines_for_meta(), collect_notes_files(), typing.Any, join_frontmatter(), split_first_frontmatter())?
1. How does 'scripts_migrate_notes_flat_py_restore_original_path_line' relate to 3 different communities (rewrite_notes_paths(), typing.Any, yaml_quote())?

---
_Generated by graphify-rs_
