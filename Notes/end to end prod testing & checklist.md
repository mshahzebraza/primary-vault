---
status: reference
tags:
  - checklist
  - testing
original_path: "Notes/Work/aiquery.io/end to end prod testing & checklist.md"
base: Work
organization: "[[aiquery.io]]"
categories:
  - "[[Work]]"
  - "[[aiquery.io]]"
---

## Feature Testing Notes

### Rapid Response
- Setup UX/UI for the view
- Meant only for quick testing
- No filters required
- No table actions required

### Create Query View
- (details TBD)

### Custom Extension
- (details TBD)

### Liveshell
- (details TBD)

---

## End-to-End Prod Checklist

### 1. Tenant Setup
- [ ] Switch to prod environment
- [ ] Use the admin infra login endpoint to get a token
- [ ] Create a tenant
- [ ] Invite the root user

### 2. Console Setup
- [ ] Change account name (optional)
- [ ] Setup feature flags
- [ ] Invite users / team members
- [ ] Create API Roles / Keys

### 3. Core Feature Verification
- [ ] Register an agent
- [ ] Run a query on the agent
- [ ] Create an agent group
- [ ] Register agent with the agent group
- [ ] Run a query on the agent group
- [ ] Test liveshell

## Related Notes
- [[PPE to PROD checklist]]
- [[Tasks Manifest - Ai Query]]
