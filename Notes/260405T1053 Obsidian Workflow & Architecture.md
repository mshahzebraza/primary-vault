---
tags:
- journal
date: 2026-04-05
---
## Work Related
3 Primary Bases
- Tasks
- Meetings
- HQ (Multiple Views: Organization grouped with projects,)



## Properties
- Organization: [[aiquery.io]] | [[scholarbee]]
- Projects: [[aq-client]] | [[aq-infrastructure]] | [[sb-backend]] | [[sb-ops-scripts]] | [[sb-frontend-student]] | [[other/misc]] (when the note isn't scoped to any project)
- Meetings: 
- Type: [[Journal]] (for meetings) | [[Idea]] | [[Task]]
- Categories: [[Meetings]] | [[Documentation]] | [[Scrum]] | [[Task]]
- Tags: `tech-learning`, `linux-pc-setup`, `open-claw`, `ossu`, `solar-system`, `cs-notes`, `search-engines`, `backend`, `frontend`, `AI`, `automation`, `dotfiles`, `legal`, `resources` etc. (they should not be code though)
### Templates
Proper Templates should be created and be documented somewhere on how to use and how and when to insert into notes etc (the complete usage workflow)

## Todos/Instructions
- The categories should all be added as internal links in the properties
- The tags should not be internal links
- We need to clearly define the distinction and usage of the `Categories` and `Tags`
- Tasks & Topics are canonical and should be de-duplicated
- base and original file path are legacy properties and should be removed after correct linking is established between notes
- unnecesary categories notes should be removed and be kept to a minimum
- use standard names for properties to avoid mutliple names for same properties i.e. `created_at` and `date`
- each of the organization should have their own 
- caterogry(...), organization, type(meeting, journel, task), status, date, project, tags and optionally topic should be the core properties.
- tags should include the things like `tech-learning`, `linux-pc-setup`, `open-claw`, `ossu`, `solar-system`, `cs-notes`, `search-engines`, `backend`, `frontend`, `AI`, `automation`, `dotfiles`, `legal`, `resources`
- think of tags like a inferior and scattered version of categories. If we notice a tag being used too many times, we can promote it to a category page of its own. Otherwise, there'd be a single tags note, with tabs for all the individual tags (or custom grouped) 
- There should be a way (preferrably a base) to view all the avilable categories and tags, which should be clickable to view all the notes linked to that specific tag or category.
- Moreover, a flow should be documented to merge multiple tags into one for standardization or when we need to promote a `tag` to `category`.
- a Readme file should also be created to document how to approach the navigation, note-taking etc.
- Daily notes are not to meant be filled manually. They are just to serve as the hub for all the notes taken for the day. And should be created automatically in the `<root>/Daily`

## Workflows/Scenarios
User comes to obsidian
Opens the Task Manifest Base which can have multiple tabs for each of the organizations.

Almost all tasks are initiated withing meetings. So, We just add the meeting notes and try adding/using the internal links for possible tasks (either existing or new). Then ask the AI to link the meetings to the relevant tasks (create new notes for tasks if not available), validate/check the metadata. 
Meetings and tasks would have many to many relation and therefore, each of their notes would have a mini base to reference the related tasks and related meetings respectively.
After the processing, the tasks should have a chronological list of actions/updates and a consolidated action item sections.


Following are a few flows that need to be handled and documented so that we clearly know how we'd be able to use the vault to cater to them. Some of them might be canonical to each other 
1. When in a meeting
2. Setting up a task independently
3. When need to add documentation for vault maintenance, rules, etc.
4. when documenting a personal setup like setting up open-claw, dotfiles, documenting solar installation etc
5. when need to record updates to a task or find the current action items/todos against a task
6. when recording r&d
7. record project updates i.e. when a freelance client timeline is updated, payment is added, requirements are submitted