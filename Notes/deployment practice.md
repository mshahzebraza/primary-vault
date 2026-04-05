---
status: reference
tags:
  - devops
  - reference
  - - Docs
original_path: Notes/Work/scholarbee/Docs/deployment practice.md
base: Work
organization: "[[scholarbee]]"
path_area: Docs
categories:
  - "[[Work]]"
  - "[[scholarbee]]"
  - "[[Docs]]"
  - "[[Projects]]"
---

## Branch → Environment Mapping

### University Portal
| Branch | Purpose | Deployment Target |
|--------|---------|-------------------|
| `dev` | Development work only | Not auto-deployed |
| `master` | Dev deployment | `web-frontend-university` |
| `staging` | Production deployment | `university-frontend-staging` |

PRs required: `dev` → `master`, then `master` → `staging`

### Student Portal
| Branch | Purpose | Deployment Target |
|--------|---------|-------------------|
| `development` | Development | `web-frontend` |
| `production` | Production | `student-frontend-staging` |

### NestJS Backend Server
| Branch | Purpose |
|--------|---------|
| `develop` | Development |
| `staging` | Production |

## Related Notes
- [[Scholar Bee Work Resources]]
