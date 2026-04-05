---
status: active
tags:
- architecture
- RnD
organization: '[[aiquery.io]]'
categories:
- '[[Work]]'
- '[[aiquery.io]]'
- '[[Tasks]]'
type: '[[RnD]]'
projects: []
priority: P2
---

## Overview
Architecture improvement questions raised during the filtering implementation. Each item below is an open refactor opportunity.

## Open Questions

- Can we stop burdening `useCreateFilterFormConfiguration` with datalist parsing? It should only be responsible for extracting config, not inferring dynamic column data types — that inference should happen upstream.

- Can we extract config from the column config before feeding anything to the store, so the store only keeps the minimum necessary data?

- Can we implement a per-view hook that resets on-mount (initial) filters when the query-response is empty?
	- Required because: for dynamic data, the filter sidebar can't be shown until data is received. If pre-applied filters cause no data to return, the user is stuck on an empty view with no way to see or reset the filters.

## Related Notes
- [[Filtering Optimization]]
- [[Filtering V2 - Athena, Clickhouse and MongoDB]]
- [[Feature Planning - Date Filters]]
