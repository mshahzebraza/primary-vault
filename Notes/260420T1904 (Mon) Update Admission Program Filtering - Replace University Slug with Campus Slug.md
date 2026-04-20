---
type: "[[Task]]"
categories:
  - "[[Work]]"
  - "[[Tasks]]"
date: 2026-04-20
tags:
  - backfilling
  - script
organization:
  - "[[scholarbee]]"
projects:
  - "[[sb-ops-scripts]]"
status:
  - active
priority: P1
---

## Context & Problem Statement**
> Currently, the Admission Program detail page identifies records using a combination of `program title` (from the program template), `city name`, and `university name`. This combination does not guarantee a unique result because a single university can have multiple campuses in the same city offering the exact same program. To fix this, we need to target the specific campus rather than the broader university entity. 
> 
> Additionally, the way we currently generate the `campus_slug` is bloated and includes redundant information that breaks our new URL architecture.

## Description
**1. Functional Requirements**

* **A. Switch from University to Campus Filtering:**
  * Replace the existing `university_name` (or `university_slug`) filtering logic with `campus_slug` filtering. 
  * This ensures we are targeting a specific campus's offering and properly resolving duplicates within the same city.

* **B. Campus Slug Normalization:**
  * **Current Behavior:** The `campus_slug` is currently generated as a merged string of `normalized(campus_name, university_name, city)`.
  * **New Behavior:** Update the generation/normalization logic so that the `campus_slug` is derived **only** from the `normalized(campus_name)`. 
  * *Reasoning:* Since the city and university information will already be handled by the route/path hierarchy or other parameters, baking them into the campus slug creates redundancy and unnecessarily long URLs.

**2. Technical Implementation Notes**
* Deprecate or gracefully handle the old university-based query structure to ensure backward compatibility during the rollout phase.
* **Migration Alert:** Because we are changing the normalization logic for the `campus_slug`, existing campus records in the database will need to have their slugs regenerated/updated to match the new `normalized(campus_name)` format.
## Current Tasks
- [ ] Create a prompt based on the curent task/note description
	- [ ] Create a mongosh script
	- [ ] 

