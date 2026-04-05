---
status: active
tags:
  - checklist
original_path: Notes/Work/aiquery.io/Tasks/PPE to PROD checklist.md
base: Work
organization: "[[aiquery.io]]"
path_area: Tasks
categories:
  - "[[Work]]"
  - "[[aiquery.io]]"
  - "[[Tasks]]"
---

## Deploy Checklist (PPE → PROD)
- [ ] Verify latest feature deployment is included
- [ ] Verify everything is working end-to-end
- [ ] Ensure `clickhouse` queues are added to prod

---

## Pending Tasks (surfaced during PPE testing)

### Settings / Teams
- [ ] Task: Add a refresh button to the Settings/Teams Table
- [ ] Task: Rename "Company" Tab → "Tenant" + Add a `tenant-id` field
- [ ] Task: Remove search from team settings view, or fix it
- [ ] Bug: First click on dropdown doesn't work in team settings

### Memberships & Auth Flow
- [ ] Bug (Frontend + Backend): Memberships need to be fetched on app-start with role details (`user built-in`, `root`) — replace current `user_type` property from `auth/user` API

**Current broken flow:**
1. User logs in → `GET /auth/user`
2. `GET /memberships` to list all memberships for `userId`
3. User selects membership → `tenantId` stored
4. `GET /memberships` is called again with `X-Tenant-ID` header (redundant, returns same list)
5. `user_type` from `GET /auth/user` is used for subsequent requests

**Expected flow:**
- `user_type` from `GET /auth/user` should NOT be used
- After membership selection → retrieve role via `GET /role/:roleId` OR `GET /memberships/:selectedMembershipId` with full detail
- First role from selected membership replaces `user_type`

### Future
- [ ] Task: Role Elevation functionality
