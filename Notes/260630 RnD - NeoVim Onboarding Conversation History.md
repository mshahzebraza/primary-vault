---
type: "[[RnD]]"
organization: 
categories: "[[Personal]]"
status: done
priority: 
date: 2026-06-30
tags: neovim, learning, onboarding, conversation-log, editor-migration, vim-grammar
read: 
url: 
---

# NeoVim Onboarding Conversation History

Learning log documenting the journey from Cursor to NeoVim. This record preserves the context, questions, and guidance from the onboarding conversation.

---

## Initial Context

**Goal**: Transition from Cursor (AI-powered IDE) to NeoVim as daily driver.

**Comfort Level**: 
- Basic arrow key navigation (`h`, `j`, `k`, `l`)
- Vague knowledge of word movements (`w`, `e`, `b`)
- Custom keybindings from YouTube tutorial (unclear what they do)

**Concerns**:
- Can Cursor's AI agent run in NeoVim?
- Can I see file diffs as clearly as in Cursor?
- Can I search for files with the same clarity?
- Git workflows (reviewing, diffing, staging) vs. Cursor's IDE integration
- Plugin mysteries—what do the installed packages actually do?
- What's fundamentally different about using NeoVim vs. an IDE?

---

## Turn 1: The Verdict

### Cursor vs. NeoVim—Myth Busting

| Feature | Cursor | NeoVim | Solution |
|---------|--------|--------|----------|
| AI Agent / Chat | Built-in | ✅ Yes | `avante.nvim`, `CodeCompanion.nvim` |
| File Search (Cmd+P) | Native | ✅ Yes | `Telescope.nvim`, `fzf-lua` |
| Git Diffs & Staging | Integrated | ✅ Yes | `gitsigns.nvim`, `Diffview.nvim`, `Neogit` |
| File Tree / Sidebar | Native | ✅ Yes | `neo-tree.nvim`, `nvim-tree.lua` |

**Bottom line**: You can replicate almost everything Cursor does in NeoVim, often *faster* and entirely keyboard-driven.

### The Mental Shift: Grammar Over Shortcuts

NeoVim doesn't ask you to memorize random keybindings. Instead, you learn a **grammar**:

**Verb + Noun/Motion**
- `dw` = Delete to next word
- `ciw` = Change inside word
- `y$` = Yank to end of line

This is composable and memorable—a radical departure from the IDE shortcut model.

### Day 1 Practice Exercises

1. **Core movements**: `h`, `j`, `k`, `l` (home row, no arrow keys)
2. **Words & lines**: `w`, `e`, `b`, `0`, `$` (word boundaries, line edges)
3. **Search-jump**: `/` (find and jump to text)

---

## Turn 2: Configuration Analysis

### What the User Provided
- `~/.config/nvim/init.lua`
- `~/.config/nvim/lua/settings.lua`
- `~/.config/nvim/lua/plugins.lua`

### Key Findings

**Leader Key**: Spacebar (`<leader>` = Space)

**Installed Plugins**:
- `nvim-tree` — File explorer sidebar
- `telescope.nvim` — Fuzzy file/text search (Cmd+P replacement)
- `gitsigns.nvim` — Git change indicators in the margin
- `Comment.nvim` — Fast line/block commenting
- `nvim-surround` — Edit surrounding delimiters (`cs"'`)
- `indent-blankline` — Visual indent guides

**Core Settings**:
- Relative line numbers (jump by distance, not absolute count)
- Screen centering on scroll (`zz`)
- System clipboard sync (yank/delete ↔ system clipboard)
- Buffer management (files in background, not visual tabs)

### Practice Exercises for Integration

**Exercise 1**: Sidebar & Window Navigation
- Launch NeoVim
- Hit `<leader>e` to toggle file tree
- Navigate with `j`, `k`; expand/collapse with `Enter`
- Jump between sidebar and editor: `Ctrl+h` (left), `Ctrl+l` (right)

**Exercise 2**: Project Navigation (Telescope)
- Hit `<leader>ff` to search files
- Type filename; navigate results with arrow keys
- Open file with `Enter`
- Cycle between buffers: `<leader>bn` (next), `<leader>bp` (previous)

**Exercise 3**: Text Editing Superpowers
- Comment a line: `gcc`
- Change quotes: `cs"'` (change surrounding `"` to `'`)
- Save file: `<leader>w`

---

## Identified Gaps (Not Yet Configured)

1. **LSP (Language Server Protocol)** — Missing code autocomplete, error checking, go-to-definition
   - Plugins: `nvim-lspconfig`, `nvim-cmp` (completion), `mason.nvim` (server installer)

2. **AI Integration** — No AI chat/agent yet
   - Plugins: `avante.nvim` (Claude integration), `CodeCompanion.nvim` (general LLM)

3. **Telescope Navigation Issue** — `Ctrl+j`/`Ctrl+k` ignored in Telescope picker
   - Solution: Custom `config` function in `plugins.lua` to override Telescope's default keymaps

---

## Next Steps

- [ ] Practice drills (Exercises 1–3 daily for 5–10 minutes)
- [ ] Decide: Expand configuration now or practice core movement first?
- [ ] If expanding: Add LSP for autocomplete
- [ ] If expanding: Add AI plugin (avante.nvim for Claude)
- [ ] Fix Telescope keymaps to use `Ctrl+j`/`Ctrl+k`

---

## Related Notes

- [[260630 Documentation - NeoVim Personal Guide & Cheat Sheet]] — Full keybinding reference and practice workflows
