---
type: "[[Meeting]]"
categories:
  - "[[Meetings]]"
  - "[[Work]]"
date: 2026-04-15
tags:
  - journal
organization:
  - "[[scholarbee]]"
projects:
  - "[[aq-backend]]"
attendees:
  - "[[M. Arsalan]]"
  - "[[Aliza Sabahat]]"
---

## Context
> On the request of Mr. Haroon and Mr. Usman, signup flow needs to be simplified
## Discussion
- signup will replace first name and last name with full name
- applications will still accept both names, but keep last name optional

## Action Items
- [x] first name + last name -> fullname in user schema
- [ ] [[#make application credentials accept optional lastname]]
- [ ] documents + toc validation removal
- [ ] auto signup by sending tokens on signup
- [ ] test all flows


### make application credentials accept optional lastname
- updated application snapshot to require first and last name from user
	- **Problem:** user might not already have the 2 fields. 
		- Option 1: If we decide to accept it in application DTO, then user might input information each time differently. 
		- **Option 2:** Otherwise, we can prompt the user to save first name and last name in the profile completion on frontend, if not already completed. This is appropriate UX because we already show the steps for profile completion at the time of application
- 