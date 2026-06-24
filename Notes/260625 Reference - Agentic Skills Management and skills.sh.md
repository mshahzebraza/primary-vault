---
type: "[[Reference]]"
categories:
  - "[[Personal]]"
  - "[[TechLearning]]"
tags:
  - agentic-ai
  - skills
  - workflow
  - claude-code
date: 2026-06-25
read: false
url: https://www.skills.sh/
---

## What is skills.sh?

[skills.sh](https://www.skills.sh/) is an open marketplace for reusable AI agent skills — pre-built procedural knowledge modules that can be installed into agents like Claude Code, Cursor, GitHub Copilot, Windsurf, and 20+ others with a single command.

> "Skills are reusable capabilities for AI agents" — an open-source approach to extending agent functionality systematically across platforms.

As of mid-2025 it hosts 700k+ skills. Skills are organized by topic (React, Next.js, Design & UI, Databases, Testing) and vetted via security audits. Notable publishers include Vercel Labs and Matt Pocock.

---

## How skills work — the npx skills model

The `npx skills` CLI (by Vercel Labs) functions as a **package manager for AI agent behaviors**.

### File structure

Each skill repository contains:

- **`SKILL.md`** — the entry point: name, description, tool definitions, and prompt instructions telling the agent when and how to use the skill
- **`.skills.json`** — the dependency manifest (analogous to `package.json`)
- **`skills-lock.json`** — the lock file (analogous to `package-lock.json`)
- **`.agents/skills/`** — the install directory (analogous to `node_modules/`)

GitHub serves as the registry; any public repo with a `SKILL.md` is installable.

### Essential commands

```bash
npx skills add microsoft/playwright-cli   # install a skill
npx skills list                           # list installed skills
npx skills update                         # update all
npx skills init my-skill                  # scaffold a new skill
npx skills experimental_install           # CI-safe install from lock file
```

### Known gotcha

The `remove` command removes skill files but leaves the entry in `skills-lock.json`. Requires manual cleanup of `.skills.json` and lock regeneration.

---

## How teams integrate skills into their workflows

### Per-project skills

Skills installed via `npx skills add` are scoped to the project. Teams commit `.skills.json` and `skills-lock.json` to the repo so every developer and CI run gets the same agent behaviors.

### CI/CD consistency

Add `npx skills experimental_install` to CI pipelines to ensure consistent skill versions across all environments — same idea as `npm ci`.

### Custom organization skills

Any private repo with a `SKILL.md` works the same way. Teams build and share internal skills (deployment workflows, code review checklists, migration scripts) without publishing to the public registry.

### Daily dev workflow

1. `npx skills list` to see what's active in the current project
2. Trigger skills by their defined phrases (e.g., `/resolve-meeting`, `/vault-audit`) during agent sessions
3. `npx skills update` periodically to pull improvements from upstream skill authors

---

## Comparison: npx skills vs. manual SKILL.md approach

This vault uses a manual approach: skills live in `.claude/skills/<name>/SKILL.md` and are loaded by Claude Code automatically as project-scoped context. The npx skills model adds:

| Feature | Manual `.claude/skills/` | `npx skills` |
|---------|--------------------------|--------------|
| Discovery | By hand | Marketplace at skills.sh |
| Versioning | Git history only | `skills-lock.json` |
| Sharing | Copy files | `npx skills add owner/repo` |
| Updates | Manual copy | `npx skills update` |
| CI consistency | Manual | `experimental_install` |

For a personal vault with custom skills, the manual approach is simpler. For team projects with shared tech-stack skills (Playwright, Prisma, Next.js), `npx skills` reduces per-project setup cost significantly.

---

## Related

- [[260625 Documentation - Vault AI Workflow Skills Guide]] — how this vault's own skills are structured
- [skills.sh](https://www.skills.sh/)
- [dev.to: Managing AI Agent Skills with npx skills](https://dev.to/toyama0919/managing-ai-agent-skills-with-npx-skills-a-practical-guide-2an8)
