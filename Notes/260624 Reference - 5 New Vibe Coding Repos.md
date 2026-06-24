---
type:
  - "[[Reference]]"
categories:
  - "[[Personal]]"
  - "[[TechLearning]]"
date: 2026-06-24
url: https://www.youtube.com/watch?v=UnzD_bwylWs
source: "YouTube — Sean Kochel"
read: true
tags:
  - ai-tools
  - agentic-workflow
---

# 5 New Vibe Coding Repos (Sean Kochel)

Video covers 5 GitHub repos that improve AI-assisted (vibe coding) workflows. Core theme: build a **learning loop** — use automation to understand your codebase, not just ship faster.

## Tools

### 1. Draw.io Skill
Generates architecture diagrams from your codebase — visualise how services and DBs connect. Useful for onboarding, debugging, and understanding unfamiliar projects.

### 2. Ponytail
Anti-overengineering auditor. Flags unnecessary complexity, files to delete, or components to shrink. YAGNI enforcer. **Already active in this vault's Claude setup.**

### 3. Handy
Free, open-source speech-to-text (alternative to Whisper Flow). Dictate context/thoughts directly into the model — faster than typing and preserves intent depth.

### 4. Improve
Codebase auditor that identifies where deterministic (cheap) logic has been replaced by LLM calls (expensive). Produces a refactor plan to reduce AI reliance where unnecessary.

### 5. Skill Spector (Nvidia)
Security auditing toolkit — scans repos for vulnerabilities. Most useful before integrating an unfamiliar library into your own project.

## Relevance to My Workflow
- **Ponytail** → already in use
- **Improve** → worth running on any LLM-heavy project to audit where inference is overused
- **Handy** → consider for rapid context dumps during planning sessions
- **Skill Spector** → run before adopting new Claude skills or MCP servers
