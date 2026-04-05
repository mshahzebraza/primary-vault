---
severity: high
status: open
tags:
- bug
original_path: Notes/Work/aiquery.io/Tasks/BUG - Race condition on custom extension Test & Publish tab.md
base: Work
organization: '[[aiquery.io]]'
path_area: Tasks
categories:
- '[[Work]]'
- '[[aiquery.io]]'
- '[[Tasks]]'
type: '[[Bug]]'
projects: []
priority: P2
---

## Description
Race condition on the Custom Extension "Test & Publish" tab. Occurs specifically when the "Test Query" input is edited.

**Location:** Custom Extension → Test & Publish tab → Test Query input

## Observed Behaviour
- `query-response-data` API is called **before** `query-response` — this should be the opposite order.

## Steps to Reproduce
1. Open a Custom Extension in the "Test & Publish" tab
2. Edit the "Test Query" input field
3. Observe network requests — `query-response-data` fires before `query-response`

## Known Sub-tasks
- Change the Test Query LIMIT to 20

## Root Cause

## Solution / Fix

## Notes
