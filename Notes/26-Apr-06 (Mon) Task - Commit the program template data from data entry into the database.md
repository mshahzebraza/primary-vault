---
type:
  - "[[Task]]"
categories:
  - "[[Work]]"
  - "[[Tasks]]"
organization:
  - "[[scholarbee]]"
projects:
  - "[[sb-ops-scripts]]"
status:
  - active
priority: P2
date: 2026-04-06
---

## Overview
> Data Team has submitted the review json, it not needs to be committed into the DB and elastic search to updated

## Current Tasks
- [ ] File Sanity and Placement
	- [ ] Place files in html
	- [ ] Review one file
	- [ ] run the script
- [ ] Unique Title Issue
	- Delete the source docs before creating the Canonical Template.  
- [ ] Unique seo Title Issue
	- [ ] The templates other than the cluster may also contain the seo title of the resolved canonical template
- [ ] Review the ingestion to ensure that `reviewed.json` files are also ingested properly


## Progress
To avoid conflicts  of name and seo-title with the sources of the same cluster, we delete the sources and then attempt the insert. However, there may be scenario where we delete  the sources of the cluster 1 and attmept the insert of cluster-1-resolved-templates but 
- it gets in conflict with the cluster-2-source-1 template.
	- This should be resolved if 
		- we ensure that none of the resolved templates across all the clusters across all files are in confict with each other AND
		- then we carry out a bulk deletion of source templates and storing their IDs and mapping them to their respective cluster-resolved-template-data. AND
		- then we perform the bulk insertion of the resolved templates
- it gets in conflict with a program template that is not yet submitted for review at all *highly unlikely*
###  SEO Title Duplication Issue

If the 






![[Related Meetings.base]]
