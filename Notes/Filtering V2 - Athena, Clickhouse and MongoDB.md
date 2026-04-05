---
status: active
tags:
  - RnD
  - feature
organization: "[[aiquery.io]]"
categories:
  - "[[Work]]"
  - "[[Tasks]]"
type: "[[RnD]]"
projects:
  - "[[aq-backend]]"
  - "[[aq-client]]"
priority: P2
---

## Overview
Upgrade the filtering system to support Athena, Clickhouse, and MongoDB with a unified abstraction layer.

## Open Research Questions
- Numbers may need first-class support — `osquery` doesn't return number type
- Look into columnar DBs and how Athena and Clickhouse work
- Query diffs to be put in Athena
- Design abstraction logic using MongoDB decorators that also works for Clickhouse

## Implementation Breakdown

### Phase 1: Query Builder Component
- [ ] Setup the Query Builder Component

### Phase 2: Filter Sidebar V2 Integration
- [ ] `FilterSidebarLayout` wraps Charts and Devices Views — account for this
- [ ] Integrate handler into filter config store
	- filter config store, its provider, and config setup hooks all need updating
	- `useManualFilters` and the filter-schema structure used across the app will change

### Phase 3: Hooks Integration
- [ ] Integrate with existing filter hooks

### Phase 4: API Integration
- [ ] Integrate with API layer

## Notes
- Take a look at P0 tasks first before starting this

## Related Notes
- [[Filtering Optimization]] — core Filter type definition
- [[Possible Areas to Update of Filtering Architecture]]
- [[Feature Planning - Date Filters]]
