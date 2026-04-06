---
type:
  - "[[Task]]"
categories:
  - "[[Work]]"
  - "[[Tasks]]"
organization:
  - "[[scholarbee]]"
projects:
  - "[[sb-backend]]"
status:
  - backlog
priority: P2
date: 2026-04-06
---

## Overview
> One paragraph describing what and why.

- program templates will be controlled by scholarbee
- if a university needs to create a program which is not available in the program templates list, they'll contact the tech support
- Proposed & Rejected: Allow University Admins to create their own templates
	- University Admins should be able to create their own templates, which would be bound to the university and be only available for use across the specific university along with the global [[Program Templates]]
	- At regular intervals, tech support will analyze the list of Program Templates owned by the universities, and promote them to scholarbee ownership to be displayed to all clients
	- Pros: University Admins don't have to wait on scholarbee for entry,
	- Cons: In case of same templates created by multiple universities, conflicts would need to be resolved when we upgrade the templates to scholarbee ownership. Or we'd have to choose between promoting only one of the duplicates. Which would mean that non-promoted template will still show up as duplicate in the template list.
	- For now the complexity to implement exceeds the benefits of dual ownership feature of program templates. 
## Current Tasks
- Ensure that University can lookup on the program templates to choose a template for program creation

![[Related Meetings.base]]
