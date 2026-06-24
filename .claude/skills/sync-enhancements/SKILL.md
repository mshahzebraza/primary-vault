---
name: sync-enhancements
description: Scan task notes and sync the has-enhancements frontmatter flag. Use when the user says "sync enhancements", "update enhancement flags", "which notes have open enhancements", or after completing a sprint/task to keep the Enhancement Backlog base accurate.
---

# sync-enhancements

Reads every task/bug note, checks whether `## Enhancements` contains open `[ ]` items, and writes `has-enhancements: true/false` accordingly. Read-only until the update step; reports changes before writing.

## Steps

### 1. Scan

```python
import os, re, yaml

notes = "Notes/"
ENHANCEMENTS_RE = re.compile(r'## Enhancements(.+?)(?=\n## |\Z)', re.DOTALL)
OPEN_ITEM_RE    = re.compile(r'- \[ \]')

results = []
for fn in os.listdir(notes):
    if not fn.endswith('.md'): continue
    txt = open(os.path.join(notes, fn)).read()
    # parse frontmatter
    if not txt.startswith('---'): continue
    end = txt.find('\n---', 3)
    if end == -1: continue
    fm_raw = txt[4:end]
    try: fm = yaml.safe_load(fm_raw)
    except: continue
    if not fm or fm.get('type') not in (
        [{'__ref': 'Task'}], '[[Task]]', [['Task']]
    ):
        pass  # still process — check by string match below

    # Only process Task / Bug / RnD notes
    type_val = str(fm.get('type', ''))
    if not any(t in type_val for t in ('Task', 'Bug', 'RnD')): continue

    m = ENHANCEMENTS_RE.search(txt)
    has_open = bool(m and OPEN_ITEM_RE.search(m.group(1)))
    current_flag = fm.get('has-enhancements', None)
    results.append((fn, has_open, current_flag))
```

### 2. Report

Print a summary before writing:
- Notes where `has-enhancements` will be set to `true` (open items found)
- Notes where `has-enhancements` will be set to `false` (section empty or all done)
- Notes with no `## Enhancements` section (skip — do not add the field)
- Notes already in sync (no change needed)

### 3. Update frontmatter

For each note that needs a change, update `has-enhancements` in-place using a YAML-safe regex replace (do not rewrite the whole frontmatter block). Only touch notes that already have the `## Enhancements` section — never add the field to notes that lack the section.

```python
def set_flag(path, value):
    txt = open(path).read()
    end = txt.find('\n---', 3)
    fm_block = txt[4:end]
    if 'has-enhancements:' in fm_block:
        new_fm = re.sub(r'has-enhancements:.*', f'has-enhancements: {str(value).lower()}', fm_block)
    else:
        new_fm = fm_block.rstrip() + f'\nhas-enhancements: {str(value).lower()}\n'
    open(path, 'w').write('---\n' + new_fm + '\n---' + txt[end+4:])
```

### 4. Confirm

Report:
- Count of notes updated to `true`
- Count of notes updated to `false`
- Count of notes skipped (no Enhancements section)
- Count already in sync

Remind the user to open `Enhancement Backlog.base` to review the flagged notes.
