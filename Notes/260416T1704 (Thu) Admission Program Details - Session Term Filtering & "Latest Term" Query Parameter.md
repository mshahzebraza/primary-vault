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
  - completed
priority: P2
---
## Overview
> Currently, the Admission Program detail page identifies records using a combination of `program title` (from the program template), `city name`, and `university name`. This combination does not guarantee a unique result because a single university can have multiple campuses in the same city offering the exact same program. 

Jira Ticket: https://scholarbee-team.atlassian.net/browse/SB-1404

## Description
**1. Context & Problem Statement**
To guarantee absolute uniqueness for an admission program record, we must account for the specific admission session (term and year). However, for SEO purposes, we want to reuse the exact same frontend URL every year. 

The target SEO-friendly URL structure is planned as:
`{program-template.title}-{admission.session.term}/{admission.campus.address.city}/{admission.campus.name}`
*(Example: `bs-computer-science-fall/karachi/nust-pnec`)*

Notice that the year is intentionally omitted from the URL. The backend must facilitate querying by these session parameters without relying on the year being present in the URL path.

**2. Functional Requirements**

* **A. Session Term & Year Filtering:**
  * The backend API must support querying by `session_term` (season) and `session_year`.
  * **URL Constraint:** The year must not be exposed in the frontend URL routing to maintain evergreen URLs year-over-year. Instead, the frontend client will dynamically inject the relevant year into the backend API request as a hidden query parameter.

* **B. "Latest Term" Query Parameter:**
  * Introduce a new query parameter on the endpoint: `only-latest-term-programs` (boolean).
  * **Behavior:** When the frontend passes `only-latest-term-programs=true`, the backend should ignore any specific year parameters. Instead, it must automatically resolve and return the admission program record for the most recent/latest available year for that specific program/campus combination.

**3. Technical Implementation Notes**
* Ensure the DB query efficiently groups or sorts by date/year to accurately and quickly fetch the "latest" record when the `only-latest-term-programs` flag is active.
## Current Tasks
- [x] Allow search of campus slug in detail list
- [x] update the schema of admissions collection
- [x] inspect the admission collection to check if it contains fall|spring 202x pattern or not.
- [x] create a script extract the information from the admission titles & save it in new fields
	- [x] extract the admission documents which couldn't retreive the new field information or had missing information and submit the list to PM
- [ ] allow searching of admission program detail list based on the new fields