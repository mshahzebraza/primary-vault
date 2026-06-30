---
type: "[[Documentation]]"
organization: 
categories: "[[Personal]]"
priority: 
status: done
date: 2026-06-30
tags: neovim, editor, keybindings, configuration, reference, modal-editing
read: 
url: 
---

# NeoVim Personal Guide & Cheat Sheet

Your personalized NeoVim documentation covering modal editing philosophy, keybindings, and solutions to common navigation issues.

---

## The Core Philosophy: Modal Editing & Grammar

NeoVim uses **Modes**—you spend most of your time in **Normal Mode**, treating your keyboard as a control dashboard.

### The Grammar of Vim: Verb + Noun/Motion

#### Verbs (Actions)
* `d` : Delete (cuts to clipboard)
* `c` : Change (deletes text and drops you into Insert Mode)
* `y` : Yank (copies text to clipboard)
* `v` : Visually select text

#### Nouns / Motions (Where to apply the action)
* `w` : Move to the start of the next word
* `e` : Move to the end of the current/next word
* `b` : Move backward to the start of the previous word
* `i` : Inside (used to modify text within delimiters)
* `a` : Around (includes delimiters)
* `$` : End of the line
* `0` : Start of the line

#### Examples
* `dw` → Delete to the start of the next word
* `ciw` → Change inside word (wipes out current word and enters Insert Mode)
* `yi"` → Yank everything inside double quotes
* `d$` → Delete from cursor to end of line

---

## Your Global Settings (`settings.lua`)

* **Relative Line Numbers**: The current line shows absolute number; lines above/below show distance. Jump 12 lines down: `12j`
* **System Clipboard Sync** (`opt.clipboard = "unnamedplus"`): Any yanked or deleted text is instantly available in your system clipboard
* **The Leader Key**: Spacebar is your `<leader>` key for launching plugin panels

---

## Keybindings Reference

### Navigation & Screen Control
| Keymap | Mode | Action |
| :--- | :--- | :--- |
| `h` / `j` / `k` / `l` | Normal | Left / Down / Up / Right |
| `Ctrl + h` | Normal | Move cursor to left window |
| `Ctrl + j` | Normal | Move cursor to window below |
| `Ctrl + k` | Normal | Move cursor to window above |
| `Ctrl + l` | Normal | Move cursor to right window |
| `Ctrl + d` | Normal | Scroll down half page (centers line) |
| `Ctrl + u` | Normal | Scroll up half page (centers line) |

### Buffer (File Tab) Management
* `<leader> bn` → Switch to next buffer
* `<leader> bp` → Switch to previous buffer
* `<leader> bd` → Close current buffer

### Global Actions
* `Esc` → Clear search highlight
* `<leader> w` → Write (save file)
* `<leader> q` → Quit window/NeoVim

### Plugin Shortcuts
* `<leader> e` → Toggle NvimTree (file explorer)
* `<leader> ff` → Find files (Telescope)
* `<leader> fg` → Live grep across files (Telescope)
* `<leader> fb` → Find open buffers
* `gcc` → Comment/uncomment current line
* `gc` → Comment/uncomment visual selection

---

## Fixing Telescope Navigation (`Ctrl+j` / `Ctrl+k`)

### The Problem
Telescope's floating window overrides global keymaps. By default it uses `<C-n>` (next) and `<C-p>` (previous) for result navigation.

### The Solution: Update `plugins.lua`

```lua
-- Fuzzy finder
{
  "nvim-telescope/telescope.nvim",
  branch = "0.1.x",
  dependencies = { "nvim-lua/plenary.nvim" },
  keys = {
    { "<leader>ff", "<cmd>Telescope find_files<CR>" },
    { "<leader>fg", "<cmd>Telescope live_grep<CR>" },
    { "<leader>fb", "<cmd>Telescope buffers<CR>" },
    { "<leader>fh", "<cmd>Telescope help_tags<CR>" },
  },
  config = function()
    local actions = require("telescope.actions")
    require("telescope").setup({
      defaults = {
        mappings = {
          i = {
            ["<C-j>"] = actions.move_selection_next,
            ["<C-k>"] = actions.move_selection_previous,
          },
          n = {
            ["j"] = actions.move_selection_next,
            ["k"] = actions.move_selection_previous,
          },
        },
      },
    })
  end,
},
```

---

## Practice Drills

### Drill 1: File Explorer Integration
1. Launch NeoVim in a project directory
2. Hit `<Space> e` to open the sidebar
3. Navigate with `j` and `k`, expand/collapse with `Enter`
4. Open a file with `Enter`
5. Switch between sidebar and editor: `Ctrl + h` (left) and `Ctrl + l` (right)

### Drill 2: Project Scouting with Telescope
1. Close sidebar: `<Space> e`
2. Open file search: `<Space> f f`
3. Type filename; navigate with `Ctrl + j` / `Ctrl + k` (after applying fix above)
4. Open file with `Enter`
5. Cycle between open files: `<Space> b n` (next) and `<Space> b p` (previous)
