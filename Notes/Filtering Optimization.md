---
status: backlog
tags:
  - RnD
  - architecture
original_path: Notes/Work/aiquery.io/Tasks/Filtering Optimization/Filtering Optimization.md
base: Work
organization: "[[aiquery.io]]"
path_area: Tasks
categories:
  - "[[Work]]"
  - "[[aiquery.io]]"
  - "[[Tasks]]"
---

## Overview
Core filter type definition used across the application. This is the canonical server-side `Filter` type.

```tsx
type Filter =  
    | { and: Filter[] }  
    | { or: Filter[] }  
    | { nor: Filter[] }  
    | { not: Filter }  
    | { eq: { field: string, value: any, caseInsensitive?: false | true } }  
    | { neq: { field: string, value: any, caseInsensitive?: false | true } }  
    | { contains: { field: string, value: any, caseInsensitive?: false | true } }  
    | { regex: { field: string, value: any } }  
    | { gt: { field: string, value: any } }  
    | { gte: { field: string, value: any } }  
    | { lt: { field: string, value: any } }  
    | { lte: { field: string, value: any } }  
    | { exists: { field: string } }  
    | { isNull: { field: string } }  
    | { in: { field: string, values: any[], caseInsensitive?: false | true } }  
    | { nin: { field: string, values: any[], caseInsensitive?: false | true } };
```

## Related Notes
- [[Filtering V2 - Athena, Clickhouse and MongoDB]]
- [[Possible Areas to Update of Filtering Architecture]]
- [[Feature Planning - Date Filters]]
