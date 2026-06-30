---
type: "[[Meeting]]"
organization: "[[aiquery.io]]"
categories:
  - "[[Work]]"
  - "[[Meetings]]"
projects: []
date: 2026-06-30
attendees: []
related-tasks: []
tags:
  - query-creation
  - filters
  - tags
  - query-packs
  - schedules
---

## Context

Weekly AiQuery meeting focused on changes to existing query flows and feature enhancements for query creation, filtering, and tagging capabilities.

## Discussion
- Task 1: Create and Listing Views for Query, Query Pack, Query Schedules, And Query Pack Schedules should have support of filter-presets, tags-creation etc.
- Task 2: Changed interface of Execution Targets
```
export interface ExecutionTarget {
        agents: string[];
        agent_groups: {
            id: string;
            title: string;
        }[];
    }
```
### Changes to existing flows:
1. **Query creation checkbox** — adding a checkbox to query creation UI to ensure that the query is created separately for each of the target agent groups in the backend
2. **Tags and saved filters** — addition of tags and saved filters for query packs and schedules

## Decisions Made
- need to pass all the hard codedd filters to the preset filters creation

## Action Items
- [ ]
