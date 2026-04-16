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

## Overview
> Frontend needs a way to click on admission programs from the listing and get to the unique results. To make results narrower and unique, we need to filter the admission program detail list endpoint using the fields like "fall" and "2026".

## Current Tasks
- [ ] update the schema of admissions collection
- [ ] extract the information from the admission titles & save it in new fields
	- [ ] extract the admission documents which couldn't retreive the new field information or had missing information and submit the list to PM
- [ ] allow searching of admissin program detail list based on the new fields

## Acceptance Criteria
Frontend should be able to search the admission program with the url like:
`{bs-computer-science}-{fall}-{2026}/{karachi}/{nust-pnec}`
which behind the scenes would result with 5 query param api endpoint
