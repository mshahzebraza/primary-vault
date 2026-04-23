---
type: "[[Task]]"
categories:
  - "[[Personal]]"
  - "[[Work]]"
  - "[[Tasks]]"
date: 2026-04-23
tags:
  - optimization
  - clean-code
  - ui
organization:
  - "[[aiquery.io]]"
projects:
  - "[[aq-client]]"
status: backlog
priority: P2
---

## Overview
> instead of having to wrap the mutation functions manually, there should be an integration of toast within the useXYZQuery or useXYZAction hooks to trigger the toast, with the option to override behavior.

## Current Patterns
File: `src/application/hooks/query-export-job.hook.tsx`
```ts
static useDeleteQueryExportJob = (queryId: string) => {
	// toast wrapped mutation fn
	const toastWrappedMutationFn = useCallback((jobId: string) => {
		return toast
			.promise(QueryExportJobData.delete(jobId), {
				className: 'priority-medium',
				loading: 'Deleting query export job...',
				success: 'Query export job deleted successfully',
				error: 'Failed to delete query export job'
			})
			.unwrap();
	}, []);

```

File:  `src/client/views/query-detail/query-metadata/use-query-metadata-view.hook.tsx`
```ts

const toastWrappedQueryFn = () => {
	return toast
		.promise(
			// promise
			QueryExportJobData.download(jobId),
			// toast options
			{
				className: 'priority-medium',
				loading: 'Downloading query export job...',
				success: 'Query export job downloaded successfully',
				error: 'Failed to download query export job'
				// description(
				// 	data: IApiResponse<
				// 		IDownloadQueryExportJobDto['response']
				// 	>,
				// ) {
				// 	return `Downloading Job of ${data.data.query_export_job_id}...`;
				// }
			}
		)
		.unwrap();
};
```

File: `src/client/views/settings/team-settings/team-settings.view.tsx`
```ts

const onRefresh = () =>
	// TODO: Ensure that multiple clicks on the refresh button remove the previous toast notification as well as the query refetch request
	toast.promise(membershipsFetchQuery.refetch(), {
		className: 'priority-medium',
		loading: 'Refreshing team members...',
		success: 'Team members refreshed',
		error: 'Failed to refresh team members'
	});

```
## Intended API
```
const teamInvitesFetchQuery = useTeamInvitesList()

const onRefresh = teamsInvitesFetchQuery.refetch({
	toast: { // this refetch toast uses success toast
		enable: true, // override required becase the get-query doesn't trigger override with default config,
		promiseTitle: "Refreshing Invites"
		successTitle: "Invites Refreshed"
	}
})

```
## Current Tasks
- [ ] Plan the new api and architecture for the reusable Toast + Query/Mutation Hooks integration





![[Related Meetings.base]]
