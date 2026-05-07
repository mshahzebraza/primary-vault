---
type:
  - "[[Task]]"
categories:
  - "[[Work]]"
  - "[[Tasks]]"
organization:
  - "[[scholarbee]]"
projects:
  - "[[sb-backend]]"
  - "[[sb-frontend-student]]"
status: backlog
priority: P1
date: 2026-04-24
tags:
  - backend
  - frontend
  - admissions
  - api
  - edge-cases
---

## Overview
> Backend changes for the combined handling of **admission dates**, **`receivingApplication`**, and **status**.

This includes two coupled requirements:
- Correct admission program responses in the **rich filters API** (`withFilters`) when these properties interact (including edge cases).
- Ensure **application draft creation** and **application submission** enforce the *same* combined rules (no inconsistencies between listing vs create/submit flows).

## Current Tasks
- [ ] Document the expected truth table / rules for the combined behavior:
  - [ ] admission start/end date (including missing/partial dates and boundary behavior)
  - [ ] `receivingApplication` flag behavior
  - [ ] admission status flag behavior
  - [ ] combined interactions (date window + status + receivingApplication)
- [ ] Update backend `withFilters` implementation to match the rules and cover edge cases deterministically.
- [ ] Ensure application **draft creation** enforces the same combined rules as listing/filters.
- [ ] Ensure application **submission** enforces the same combined rules as listing/filters.
- [ ] Add automated tests covering:
  - [ ] rich filters API (`withFilters`) results (positive + negative cases)
  - [ ] application draft creation validation
  - [ ] application submission validation

## Acceptance Criteria
- [ ] `withFilters` results are correct across edge cases (including boundary dates and missing fields).
- [ ] Draft creation and submission enforce the same combined constraints as listing/filters.
- [ ] Test suite covers the combined rules so regressions are prevented.

![[Related Meetings.base]]
