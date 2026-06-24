---
type: "[[Task]]"
categories:
  - "[[Work]]"
  - "[[Tasks]]"
organization:
  - "[[aiquery.io]]"
projects:
  - "[[aq-client]]"
status:
  - completed
priority: P1
date: 2026-04-23
---

## Overview
> Currently manual swapping of lists is required for the timezones dropdown options. Moreover, in reality, the actual time of DST implementation is different for different countries.

## Current Tasks
- [x] Use IANA to compute the timezones for the selected locations dynamically on app mount. So, for locations A, B, C... so on, we'd ask IANA for current timezones instead of maintaining the timezones ourselves.


![[Related Meetings.base]]
