---
aliases:
  - Backup/Clone a MongoDB database using Mongo Tools
original_path: Notes/Tech Learning/Misc/BackupClone a MongoDB database using Mongo Tools.md
base: TechLearning
path_area: Misc
categories:
  - "[[TechLearning]]"
  - "[[Misc]]"
---
## Prerequisites
- MongoDB Community Server
- MongoDB tools
- MongoDB shell

## Script

```bash title:"clone-atlas-to-local.sh"
#!/bin/bash

# -----------------------------------------------------------------------------------
# Script to clone a MongoDB Atlas database to a local MongoDB instance
# Requires: mongodump, mongorestore, and local MongoDB running on localhost:27017
# -----------------------------------------------------------------------------------

# -----------------------------
# ✅ CONFIGURATION SECTION
# -----------------------------

# Full MongoDB Atlas connection URI
# 🔥 Expected format: mongodb+srv://<username>:<password>@<cluster>.mongodb.net/<dbname>
# 🔥 Example: mongodb+srv://myuser:myp%40ssword@cluster0.mongodb.net/myProductionDB
# ⚠️ Make sure special characters in the password are URL-encoded (e.g., @ => %40)
MONGO_ATLAS_URI="mongodb+srv://yourUser:yourEncodedPassword@cluster0.mongodb.net/yourProdDB"

# The actual DB name in Atlas to dump (this must match the name used in the URI above)
ATLAS_DB_NAME="yourProdDB"

# Local MongoDB target DB name
LOCAL_DB_NAME="yourLocalDB"

# Temporary directory where mongodump will save the backup
DUMP_DIR="prod-dump"

# -----------------------------
# 🔧 STEP 1: Dump the remote Atlas DB
# -----------------------------

echo "📦 Starting mongodump from MongoDB Atlas..."

mongodump \
  --uri="${MONGO_ATLAS_URI}" \
  --out="${DUMP_DIR}"

# Check if dump was successful
if [ $? -ne 0 ]; then
  echo "❌ mongodump failed. Exiting."
  exit 1
fi

echo "✅ mongodump completed successfully."

# -----------------------------
# 🔄 STEP 2: Restore to local MongoDB
# -----------------------------

echo "♻️ Restoring dump to local MongoDB database '${LOCAL_DB_NAME}'..."

mongorestore \
  --drop \
  --db "${LOCAL_DB_NAME}" \
  "${DUMP_DIR}/${ATLAS_DB_NAME}"

# Check if restore was successful
if [ $? -ne 0 ]; then
  echo "❌ mongorestore failed. Exiting."
  exit 1
fi

echo "✅ mongorestore completed successfully."

# -----------------------------
# 🧹 STEP 3: Clean up dump files
# -----------------------------

echo "🧽 Cleaning up temporary files..."

rm -rf "${DUMP_DIR}"

echo "✅ Cleanup complete."

# -----------------------------
# 🎉 DONE
# -----------------------------

echo "🎉 Successfully cloned '${ATLAS_DB_NAME}' from Atlas to local DB '${LOCAL_DB_NAME}'."

```

### ✅ How to Use

1. Save as `clone-atlas-to-local.sh`
2. Make executable:
   `chmod +x clone-atlas-to-local.sh
3. Edit these variables at the top:
    - `MONGO_ATLAS_URI`
    - `ATLAS_DB_NAME`
    - `LOCAL_DB_NAME`
4. Run it: `bash ./clone-atlas-to-local.sh`


Related to 
- [[MongoDB]]
- [[MongoDB Tools]]