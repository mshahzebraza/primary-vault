---
type: "[[Journal]]"
categories:
  - "[[Journal]]"
  - "[[Work]]"
date: 2026-05-09
---

## Scratch
- account settings shows the current tenant role
- syncing enabled on signin
- after export, "See Results" should show job without manual refresh; verify on PPE.
- Ensure Query Detail's Tab Queries are run only when the tab is mouted.
- in Bulk Agents Custom extension Deployments Dialog
	- Custom extension deployment per group or device select is inverted? 
	- Add pill distinction for AMD vs ARM
- Rapid Response enhancements
	- Consolidated actions menu
	- Split-button toolbar layout
	- Cancel covers all execution phases
		- POST — fire-and-forget (server will complete), but client state is cleared so downstream phases never start
		- GET — aborted at the network level via TanStack's AbortSignal → axios passthrough
		- SSE stream — aborted via AbortController
- fix the SlotClone issue caused by the `TabsContent` component's `asChild` prop in the Query Detail Tabs by using `forwardRef`.
- 
