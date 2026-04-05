---
status:
tags:
  - feature
  - RnD
  - - R&D
original_path: "Notes/Work/scholarbee/R&D/Sorting Weight Implementation.md"
base: Work
organization: "[[scholarbee]]"
path_area: "R&D"
categories:
  - "[[Work]]"
  - "[[scholarbee]]"
  - "[[R&D]]"
  - "[[Projects]]"
---

## Overview
Personalised program/scholarship feed using weighted sorting — content-based, collaborative, and deadline-based signals.

## Weighting Signals
- **Location-based (content):** programs near the user's city get higher weight — requires city-to-area/zone mapping
- **Deadline-based (time):** programs closer to deadline get higher weight — cron/time-based content signal
- **Trend-based (collaborative):** programs appearing more in searches get higher weight — feeds into other users' rankings too

## Approaches Researched

### Content-based Filtering
- Recommends programs similar to what the user has shown interest in, based on item attributes + user profile
- Good for cold-start: only needs stated preferences (degree, major, location), no historical interaction data needed

### Collaborative Filtering
- Recommends based on similarity between users ("students like you also liked…") or items
- Susceptible to cold-start for new users/programs — needs sufficient historical interaction data
- Prone to popularity bias (over-recommends popular items)

### Learning-to-Rank (LTR)
- ML paradigm — auto-assigns weights from a learned ranking function
- Elasticsearch natively supports LTR as a second-stage re-ranker

## Open Questions / Decision Points
- Should this be weighted sorting in the main feed, or separate toggle buttons (Near Me / Trending / Closing Soon)?
- Is ES LTR worth the complexity at our current data scale?
- How do we handle the cold-start problem for new users?

## Related Notes
- [[Tasks Manifest - Scholar Bee]]
