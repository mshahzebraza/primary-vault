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
  - completed
priority: P1
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
I''m not agreed on the solution of candidate and target templates with deletion. This is how I think it should be:
To avoid conflicts  of name and seo-title with the sources of the same cluster, we delete the sources and then attempt the insert. However, there may be scenario where we delete  the sources of the cluster 1 and attmept the insert of cluster-1-resolved-templates but 
- it gets in conflict with the cluster-2-source-1 template.
	- This should be resolved if 
		- we ensure that none of the resolved templates across all the clusters across all files are in confict with each other AND
		- then we carry out a bulk deletion of source templates and storing their IDs and mapping them to their respective cluster-resolved-template-data. AND
		- then we perform the bulk insertion of the resolved templates
- it gets in conflict with a program template that is not yet submitted for review at all *highly unlikely*
	- should we take a look at the non-submitted templates
- Incase of the conflict between cluster-1-resolved-template and cluster-2-source-1-template, we should just log the error explaining the issue and point to the conflicting entries and exit, instead of automatically handling the candidate and target template logic with deletion. 
- There may also be a scenario, where cluster-1-resolved-template is not in conflict with sources of other clusters yet. But it may be in conflict with the resolved-canoncial templates of other clusters, which would only surface when we start the insertion process. Like mentioned earlier, we should ensure this doesn't happen by checking all the resolved templates across all files and clusters for review, and if this conflict is found, we log and record this as the error and exit.
- The error logging for both the resolved vs subsequent cluster sources, and resolved vs subsequent cluster resolved templates, are to be recorded for all the files before exiting, instead of logging the errors for the first conflict, so that we can manually go and verify the issues and fix them in one go.
- Is there a possibility of this being caused due to data entry team adding new templates other than the recorded sources at the time of phase 1 generation

### After the Conflict Report
- reolved vs resolved: ensure that overridden ids are taken into account
- what would happen if we remove the uniqueness of properties
	- we can appent the uuid for duplicate `seo-title`
	- I think only the `seo-title-key` needs to be duplicate, title and short-name can stay as is 
- The conflict check shouldn't compare the things like name, short-name by normalizing into non-brackets lowercase strings. only lowercasing should be done, the brackets should not be dropped in normalization

- source-doc-id duplication
	- if this is ignored and allowed to go through, the impact is only for 3 documents.
	- moreover, if we update the process to ignore the dropped source docs and drop the conflicting source docs from their clusters, we'd get the source docs occuring only once in the clusters list
- resolved-templates vs resolved-templates
	- the current conflict report extracts the conflicts based on the proposed names only; while ideally the overridden proposed name should be taken into account when deciding conflict i.e. `resolved=overriden-[proposed-info] || proposed-[info]` where `info` being the any of the `name`, `short-name` and `seo-title-key` properties. Although this might not resolve the conflicts completely, it'll definitely make sure that the conflicts are correctly identified instead of false conflicts.
	- Furthermore, *there should be a UI based or a simpler approach to resolve the conflicts.*
	- if the conflicts cannot be solved we may need to merge them by manually adding the uuid suffix to conflicting `seo-title-key` values.
- resolved-templates vs db-templates
	- *...?*
	- *exclude the source docs from the checks*



![[Related Meetings.base]]
