---
status: active
tags:
- feature
original_path: Notes/Work/aiquery.io/Tasks/rapid response refactoring and enhancements.md
base: Work
organization: '[[aiquery.io]]'
path_area: Tasks
categories:
- '[[Work]]'
- '[[aiquery.io]]'
- '[[Tasks]]'
type: '[[Task]]'
projects: []
priority: P2
---

## Overview
Rapid response / live shell — SSE streaming, auth token handling, and UX enhancements.

## Current Tasks

### UX
- [ ] Show a countdown timer indicating the stream-timeout approaching
- [ ] Try to squeeze column width to content if content is smaller

### Headers & Auth
- [ ] `query-response-stream-api` should not exist — the parser should be passed in from the hook. Until then, auth headers should be set in the underlying generic stream function, or create a new authenticated SSE-stream function
- [ ] Headers should not be passed manually — the stream-subscribe method should use the default axios instance to auto-build tenant + auth headers
- [ ] Auth token should not be retrieved manually in axios requests — store it in the auth store after authentication/app-mount, and update it whenever Firebase rotates or refreshes it

**Auth store token exploration prompt:**
> I want to store the auth token in the auth store and extract it directly instead of async-getting it from Firebase SDK. It should be updated in the store whenever Firebase changes the token — on app mount, token rotation, refresh, etc. Is this possible? Is it standard practice? Any gotchas/edge cases?

## Completed

## Related Meetings
