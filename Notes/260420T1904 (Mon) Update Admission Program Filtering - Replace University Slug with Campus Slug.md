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

Jira Ticket: https://scholarbee-team.atlassian.net/browse/SB-1400
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
	- [x] Create a mongosh script
	- [x] ensure special characters are normalize and `&` is converted to `and`.
- [ ] confirm if the normalization has worked using a verification aggregation pipeline
- [ ] elastic search scriipt to ensure feed data contains the data for session

----
## Prompt
**Title:** DB Migration & Logic Update: Campus Slug Normalization and Filtering

**1. Context & Problem Statement**
Currently, the Admission Program detail page identifies records using a combination of `program title`, `city name`, and `university name`. This combination does not guarantee a unique result because a single university can have multiple campuses in the same city offering the exact same program. To fix this, we need to target the specific campus rather than the broader university entity. 

Additionally, the way we currently generate the `campus_slug` is bloated. As seen in the database, a campus name like *"Government College University Faisalabad Layyah Campus"* results in a massive, truncated slug containing redundant university and city info (e.g., `"government-college-university-faisalabad-gcuf-government-college-unive..."`). This breaks our new URL architecture.

**2. Database Schema Context (campuses collection)**
Based on the current database, the relevant fields for a campus document are:
* `_id`: ObjectId
* `name`: String (e.g., "Government College University Faisalabad Layyah Campus")
* `slug`: String (Currently bloated, needs to be regenerated)

**3. Functional Requirements**

* **A. API/Filtering Update (Switch to Campus Slug):**
  * Replace the existing `university_name` (or `university_slug`) filtering logic on the Admission Program detail endpoint with `campus_slug` filtering. 
  * This ensures we target a specific campus's offering and properly resolve duplicates within the same city.
  * *Backward Compatibility:* Deprecate or gracefully handle the old university-based query structure to ensure frontend clients don't break during the rollout phase.

* **B. Campus Slug Normalization Logic Update:**
  * **Current Behavior:** The `slug` is generated as a merged string of `normalized(campus_name, university_name, city)`.
  * **New Behavior:** Update the backend generation/normalization logic so that the `slug` is derived **only** from the `normalized(name)`. 
  * **Reasoning:** City and university information will already be handled by the route/path hierarchy. Baking them into the campus slug creates redundancy and unnecessarily long URLs.

**4. Database Migration Requirement**
* Because we are changing the normalization logic, existing campus records in the database have invalid/bloated slugs.
* **Task:** Write a MongoDB migration script (preferably a standalone `mongosh` script, or a TS script if necessary) that iterates over the `campuses` collection, takes the `name` field, runs the new normalization/slugify logic on it, and updates the `slug` field for all existing documents via a `bulkWrite` operation.