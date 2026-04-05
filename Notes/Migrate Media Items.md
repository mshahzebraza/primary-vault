---
status: active
tags:
  - task
  - script
organization:
  - "[[scholarbee]]"
categories:
  - "[[Work]]"
  - "[[scholarbee]]"
  - "[[Tasks]]"
type: "[[Task]]"
projects:
  - "[[sb-backend]]"
priority: P2
---

## Overview
Migrate media storage from the old webhook-based setup to direct GCS-Adapter integration, and fix hard-coded media URLs across all DB collections.

## Tasks

### GCS Integration
- [ ] Replace the webhook with direct GCS-Adapter integration
- [ ] Confirm credentials are correct (service account + local auth)

```env
GCS_PROJECT_ID=scholarbee-student-portal
GCS_BUCKET=scholarbee-general-assets
GCS_CLIENT_EMAIL=dummy@dummy.com
GCS_PRIVATE_KEY=dummy
```

### URL Migration Script
Hard-coded base URLs need to be fixed across these collections:

| Collection | Fields |
|---|---|
| universities | `logo_url` |
| campuses | `logo_url`, `pictures.url` |
| scholarships | `image_url`, `required_documents.document_link` |
| organizations | `profile_image_url`, `website_url` |
| blog-posts | `thumbnail` |
| users | `profile_image_url` |
| applications | `profile_image_url` |
| student-scholarships | `required_documents.document_link` |
| chat | `attachments` |

**Options to explore:**
- Option A: Replace the base URL in all affected fields via migration script
- Option B: Strip the base URL from DB; construct it dynamically at query time

## Open Questions
- When did the file migration happen?
- Is it safe to re-run the migration without creating duplicate files in storage?

## Related Notes
- [[Tasks Manifest - Scholar Bee]]
