---
type: "[[Bug]]"
categories:
  - "[[Work]]"
  - "[[Tasks]]"
date: 2026-04-19
tags:
  - journal
  - bug
organization:
  - "[[aiquery.io]]"
projects:
  - "[[aq-client]]"
status:
  - completed
priority: P1
---

## Description
> BUG: query editor gives UI jerk when content in the editor is too much due to a resizing change added earlier.

**Location:** Create Query / Schedule Dialog, Create Query / Create Preset Dialog

## Steps to Reproduce
1. Add a realistic query - you can just do select * from users, or load a preset
2. Then open save preset or schedule, the SQL editor in the pop up module should be incorrectly sized - then if you add anything at that point (space, character, etc.) you will see it snap back to the right size

## Solution / Fix
Fixed in [this PR](https://github.com/AIQuery-Project/client/pull/511) and also created [[260420T0004 (Mon) Monaco SQL Editor Height Resizing Issue Report | this report]] explaining the issue