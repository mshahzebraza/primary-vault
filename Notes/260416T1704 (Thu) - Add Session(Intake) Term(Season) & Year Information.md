---
type: "[[Task]]"
categories:
  - "[[Work]]"
  - "[[Tasks]]"
date: 2026-04-16
tags:
  - task
organization:
  - "[[scholarbee]]"
projects:
  - "[[sb-backend]]"
status:
  - active
priority: P2
---
## Title
**Feature:** Unique Admission Program Identification, Campus Slug Filtering & Latest Term Flag
## Overview
> Currently, the Admission Program detail page identifies records using a combination of `program title` (from the program template), `city name`, and `university name`. This combination does not guarantee a unique result because a single university can have multiple campuses in the same city offering the exact same program. 

Jira Ticket: https://scholarbee-team.atlassian.net/browse/SB-1404

## Description
**1. Context & Problem Statement**
Currently, the Admission Program detail page identifies records using a combination of `program title` (from the program template), `city name`, and `university name`. This combination does not guarantee a unique result because a single university can have multiple campuses in the same city offering the exact same program. 

Additionally, to guarantee absolute uniqueness, we must account for the specific admission session (season/term and year). However, for SEO purposes, we want to reuse the exact same frontend URL every year.

Therefore, final SEO friendly url might become:  
- `{program-template.title}-{admission.session.term}/{admission.campus.address.city}/{admission.campus.name}`
- `{bs-computer-science}-{fall}/{karachi}/{nust-pnec}`

**2. Functional Requirements**

* **A. Switch from University to Campus Filtering:**
  * Replace the `university_name` filtering logic with `campus_name` or `campus_slug` filtering. This ensures we are targeting a specific campus's offering rather than a broad university offering.

* **B. Session Season & Year Filtering (Under the Hood):**
  * The backend API must support querying by `session_term` (season) and `session_year`.
  * **URL Constraint:** The year must *not* be exposed in the frontend URL routing (to maintain evergreen URLs year-over-year). Instead, the frontend client will dynamically inject the relevant year into the backend API request as a query parameter.

* **C. "Latest Term" Query Parameter:**
  * Introduce a new query parameter on the endpoint: `only-latest-term-programs` (boolean).
  * **Behavior:** When the frontend passes `only-latest-term-programs=true`, the backend should ignore specific year parameters and automatically resolve and return the admission program record for the most recent/latest available year for that specific program/campus combination.

**3. Technical Implementation Notes**
* Ensure the DB query efficiently groups or sorts by date/year to accurately fetch the "latest" record when `only-latest-term-programs` is active.
* Deprecate or gracefully handle the old university-based query structure if backward compatibility is required during the rollout.

## Current Tasks
- [x] Allow search of campus slug in detail list
- [x] update the schema of admissions collection
- [x] inspect the admission collection to check if it contains fall|spring 202x pattern or not.
- [x] create a script extract the information from the admission titles & save it in new fields
	- [x] extract the admission documents which couldn't retreive the new field information or had missing information and submit the list to PM
- [ ] [[260420T1904 (Mon) Create a revised campus slug in campus collection | Create a revised campus slug in campus collection]]
- [ ] allow searching of admission program detail list based on the new fields