---
type: "[[Task]]"
categories:
  - "[[Work]]"
  - "[[Tasks]]"
date: 2026-06-24
tags:
  - feature
  - ux
  - sidebar
organization: "[[aiquery.io]]"
projects:
  - "[[aq-client]]"
status: active
priority: P2
related-tasks:
  - "[[260623 Weekly Scrum - UI Updates, Tags]]"
---

## Overview
Redesign the app sidebar (v2). Driven by the 2026-06-23 scrum. Key directions: simplify icon treatment for nested views, introduce avatar initials (Google Meet style), reshape the tenant-switching block, and align the bottom block to user identity + logout. Brand color (purple shade) applies to the sidebar.

## Phases

### Phase 1 — Figma Design
- [ ] Figma mockup for Sidebar v2
  - [ ] Icons: remove icons from nested view items, keep for top-level only
  - [ ] Avatar: initials-based avatar (Google Meet style) in the user block
  - [ ] Top block (SWITCHING): tenant name + user-role display; clicking opens tenant list as items
  - [ ] Bottom block (USER): name, email, and logout action
  - [ ] Sidebar color = brand color (purple shade)
- [ ] Review Figma with team before implementation

### Phase 2 — Implementation
- [ ] Implement Sidebar v2 from approved Figma

## Decisions
- Brand color = purple shade (decided 2026-06-23 scrum)
- Sidebar background = brand color (decided 2026-06-23 scrum)
- Sub-Tenants → deferred to future (not in v2 scope)
