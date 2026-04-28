---
type: "[[Bug]]"
categories:
  - "[[Work]]"
date: 2026-04-10
tags:
  - bug
organization:
  - "[[scholarbee]]"
projects:
  - "[[sb-ops-scripts]]"
status:
  - active
  - completed
priority: P1
---

## Description
> Document Migration Fialure for ripha university

**Logs 1:** 
```sh
❯ pnpm run migrate:dev-to-prod

> scripts@1.0.0 migrate:dev-to-prod /home/mshahzebraza/CC/dev/scholarbee/ops-scripts
> ts-node scripts/migrate-dev-to-prod.ts

[dotenv@17.2.0] injecting env (13) from .env (tip: ⚙️  override existing env vars with { override: true })

🚀 Dev to Prod Migration Script
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Source Database: scholarbee-admin-panel
Source URI: mongodb+srv://***:***@cluster0.kzgmz0i.mongodb.net/scholarbee-admin-panel
Target Database: scholarbee-backend-prod
Target URI: mongodb+srv://***:***@cluster0.kzgmz0i.mongodb.net/scholarbee-backend-prod
Collections: addresses, universities, campuses, programs, academic_departments, program_templates, admissions, scholarships, organizations, regions, countries, fees, blog_posts, fee_structures, admission_programs
Mode: ✏️  LIVE (will modify target database)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

✔ Do you want to proceed with this migration? Yes

🔌 Connecting to databases...
✅ Connected to source database: scholarbee-admin-panel
✅ Connected to target database: scholarbee-backend-prod

📊 Migration Summary:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Source: scholarbee-admin-panel (mongodb+srv://***:***@cluster0.kzgmz0i.mongodb.net/scholarbee-admin-panel)
Target: scholarbee-backend-prod (mongodb+srv://***:***@cluster0.kzgmz0i.mongodb.net/scholarbee-backend-prod)
Collections: 15
Mode: ✏️  LIVE
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

📈 Source Collection Counts:
   addresses: 706 documents
   universities: 188 documents
   campuses: 377 documents
   programs: 6365 documents
   academic_departments: 3025 documents
   program_templates: 2191 documents
   admissions: 743 documents
   scholarships: 380 documents
   organizations: 291 documents
   regions: 286 documents
   countries: 8 documents
   fees: 0 documents
   blog_posts: 4 documents
   fee_structures: 6700 documents
   admission_programs: 5757 documents
✔
⚠️  This will REPLACE existing documents in the target database. Continue? Yes

📦 Migrating collection: addresses
   Source documents: 706
   ✅ Migrated 706 documents (target now has 706 documents)

📦 Migrating collection: universities
   Source documents: 188
   ✅ Migrated 188 documents (target now has 190 documents)

📦 Migrating collection: campuses
   Source documents: 377
   ✅ Migrated 377 documents (target now has 379 documents)

📦 Migrating collection: programs
   Source documents: 6365
   ❌ Error migrating programs: E11000 duplicate key error collection: scholarbee-backend-prod.programs index: slug_1 dup key: { slug: "riphah-international-university-malakand-campus-bs-computer-science-riphah-malakand" }

📦 Migrating collection: academic_departments
   Source documents: 3025
   ✅ Migrated 3025 documents (target now has 3028 documents)

📦 Migrating collection: program_templates
   Source documents: 2191
   ✅ Migrated 2191 documents (target now has 2194 documents)

📦 Migrating collection: admissions
   Source documents: 743
   ✅ Migrated 743 documents (target now has 745 documents)

📦 Migrating collection: scholarships
   Source documents: 380
   ✅ Migrated 380 documents (target now has 380 documents)

📦 Migrating collection: organizations
   Source documents: 291
   ✅ Migrated 291 documents (target now has 291 documents)

📦 Migrating collection: regions
   Source documents: 286
   ✅ Migrated 286 documents (target now has 286 documents)

📦 Migrating collection: countries
   Source documents: 8
   ✅ Migrated 8 documents (target now has 8 documents)

📦 Migrating collection: fees
   Source documents: 0
   ⚠️  No documents to migrate

📦 Migrating collection: blog_posts
   Source documents: 4
   ✅ Migrated 4 documents (target now has 4 documents)

📦 Migrating collection: fee_structures
   Source documents: 6700
   ✅ Migrated 6700 documents (target now has 6763 documents)

📦 Migrating collection: admission_programs
   Source documents: 5759
   ✅ Migrated 5760 documents (target now has 5792 documents)


📊 Migration Summary:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
✅ Successful: 14/15
❌ Failed: 1/15
📄 Total documents processed: 20659
⏱️  Duration: 1113.35s

❌ Failed Collections:
   - programs: E11000 duplicate key error collection: scholarbee-backend-prod.programs index: slug_1 dup key: { slug: "riphah-international-university-malakand-campus-bs-computer-science-riphah-malakand" }
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

✅ Disconnected from databases
✅ Migration completed successfully!
```

**Logs 2**:
```sh
❯

pnpm run migrate:dev-to-prod > scripts@1.0.0 migrate:dev-to-prod /home/mshahzebraza/CC/dev/scholarbee/ops-scripts > ts-node scripts/migrate-dev-to-prod/index.ts [dotenv@17.2.0] injecting env (13) from .env

(tip: 🔐 encrypt with dotenvx: https://dotenvx.com)

🚀 Dev to Prod Migration Script ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ Source Database: scholarbee-admin-panel Source URI: mongodb+srv://***:***@cluster0.kzgmz0i.mongodb.net/scholarbee-admin-panel Target Database: scholarbee-backend-prod Target URI: mongodb+srv://***:***@cluster0.kzgmz0i.mongodb.net/scholarbee-backend-prod Collections: addresses, universities, campuses, programs, program_templates, academic_departments, program_templates, admissions, scholarships, organizations, regions, countries, fees, blog_posts, fee_structures, admission_programs, notification_read_receipts, notifications Mode: ✏️ LIVE (will modify target database) ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

✔

Do you want to proceed with this migration?

Yes

🔌 Connecting to databases... ✅ Connected to source database: scholarbee-admin-panel ✅ Connected to target database: scholarbee-backend-prod 📊 Migration Summary: ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ Source: scholarbee-admin-panel (mongodb+srv://***:***@cluster0.kzgmz0i.mongodb.net/scholarbee-admin-panel) Target: scholarbee-backend-prod (mongodb+srv://***:***@cluster0.kzgmz0i.mongodb.net/scholarbee-backend-prod) Collections: 18 Mode: ✏️ LIVE ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 📈 Source Collection Counts: addresses: 706 documents universities: 188 documents campuses: 377 documents programs: 6365 documents program_templates: 2191 documents academic_departments: 3025 documents program_templates: 2191 documents admissions: 743 documents scholarships: 380 documents organizations: 291 documents regions: 286 documents countries: 8 documents fees: 0 documents blog_posts: 4 documents fee_structures: 6700 documents admission_programs: 5765 documents notification_read_receipts: 661 documents notifications: 1925 documents

✔

⚠️ This will REPLACE existing documents in the target database. Continue?

Yes

📦 Migrating collection: addresses Source documents: 706 ✅ Migrated 706 documents (target now has 706 documents) 📦 Migrating collection: universities Source documents: 188 ✅ Migrated 188 documents (target now has 190 documents) 📦 Migrating collection: campuses Source documents: 377 ✅ Migrated 377 documents (target now has 379 documents) 📦 Migrating collection: programs Source documents: 6365 ✅ Migrated 6365 documents (target now has 6578 documents) 📦 Migrating collection: program_templates Source documents: 2191 ✅ Migrated 2191 documents (target now has 2194 documents) 📦 Migrating collection: academic_departments Source documents: 3025 ✅ Migrated 3025 documents (target now has 3028 documents) 📦 Migrating collection: program_templates Source documents: 2191 ✅ Migrated 2191 documents (target now has 2194 documents) 📦 Migrating collection: admissions Source documents: 743 ✅ Migrated 743 documents (target now has 745 documents) 📦 Migrating collection: scholarships Source documents: 380 ✅ Migrated 380 documents (target now has 380 documents) 📦 Migrating collection: organizations Source documents: 291 ✅ Migrated 291 documents (target now has 291 documents) 📦 Migrating collection: regions Source documents: 286 ✅ Migrated 286 documents (target now has 286 documents) 📦 Migrating collection: countries Source documents: 8 ✅ Migrated 8 documents (target now has 8 documents) 📦 Migrating collection: fees Source documents: 0 ⚠️ No documents to migrate from fees 📦 Migrating collection: blog_posts Source documents: 4 ✅ Migrated 4 documents (target now has 4 documents) 📦 Migrating collection: fee_structures Source documents: 6700 ✅ Migrated 6700 documents (target now has 6763 documents) 📦 Migrating collection: admission_programs Source documents: 5765 ❌ Error migrating admission_programs: E11000 duplicate key error collection: scholarbee-backend-prod.admission_programs index: slug_1 dup key: { slug: "graduate-fall-admission-programs-2026-lums-main-campus-ms-electrical-engineering-lums-main-campus-lums-main-campus" } 📦 Migrating collection: notification_read_receipts Source documents: 661 ✅ Migrated 661 documents (target now has 679 documents) 📦 Migrating collection: notifications Source documents: 1925 ✅ Migrated 1925 documents (target now has 2040 documents) 📊 Migration Summary: ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ ✅ Successful: 17/18 ❌ Failed: 1/18 📄 Total documents processed: 26041 ⏱️ Duration: 759.16s ❌ Failed Collections: - admission_programs: E11000 duplicate key error collection: scholarbee-backend-prod.admission_programs index: slug_1 dup key: { slug: "graduate-fall-admission-programs-2026-lums-main-campus-ms-electrical-engineering-lums-main-campus-lums-main-campus" } ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ ✅ Disconnected from databases ✅ Migration completed successfully!
```
## Steps to Reproduce
## 2026-04-10

1. Run  `pnpm run migrate:dev-to-prod`

## Root Cause

## Attempted Fixes

## Solution / Fix
- A possible fix would be to remove the unique indexes on the slugs and retry.  But we definitely have to document the root cause of it.  

## Notes

