---
type: "[[Task]]"
categories:
  - "[[Work]]"
  - "[[Tasks]]"
organization:
  - "[[scholarbee]]"
projects:
  - "[[sb-backend]]"
status: active
priority: P2
date: 2026-06-05
tags:
  - search-engine
  - elasticsearch
  - ranking
  - admission-programs
---
## Overview

Two ranking issues with the admission program search engine surfaced post-Eid. First, explicit search mode is not overriding ranking factors — a search for `SE` should pin `SE`-matching programs to the top regardless of their open/closed status, but status scoring is currently outweighing exact-match signals. Second, the `CS` search term surfaces non-partner programs before partner programs because partner titles use abbreviations like `ADCS` or `BSCS` rather than a standalone `CS` token — the tag-based boost for partners is not strong enough to overcome the non-partner exact-title match. There is a related open PR (#58 in backend-api: "feat(Search): enhancements in weightage system") that may address these.

## Current Tasks

- [ ] Investigate explicit-search mode: ensure exact-match score overrides status-based ranking factors when a user is in explicit search mode
  - [ ] Reproduce: search `SE` and confirm status-closed programs rank above explicit `SE` matches
  - [ ] Adjust ES query to apply a `filter` (not `should`) on exact match when explicit mode is active, so status boost cannot outrank it
- [ ] Investigate partner-data ranking for `CS`-like queries
  - [ ] Reproduce: search `CS` and confirm non-partner programs (with `CS` in title) outrank partner programs (with `ADCS`/`BSCS` in title and `CS` in tags)
  - [ ] Increase tag-score boost for partner programs, or add a sub-field match on abbreviation tokens, so partner results surface above non-partner exact-title matches
- [ ] Review open backend-api PR #58 ("feat(Search): enhancements in weightage system") — check if it covers either of the above and coordinate or supersede accordingly
- [ ] Test both fixes against a representative set of search terms before deploying
