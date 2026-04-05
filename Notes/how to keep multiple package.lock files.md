---
original_path: Notes/Tech Learning/Misc/how to keep multiple package.lock files.md
base: TechLearning
path_area: Misc
categories:
- '[[TechLearning]]'
tags:
- misc
---
## Problem

When company is using `yarn` and I intend to use the `pnpm`. We need to do 2 things

- Untrack the the `pnpm.lock` in `.gitignore`/`.git/info/exlude` so that our use of `pnpm` doesn't affect the rest of the team who're already using `yarn.lock`
- Delete and `untrack` the `yarn.lock` file using `.git/info/exclude`.
	- Deletion is necessary to only keep 01 `.lock` file in the repo to not cause warnings in the IDE.
	- untracking is required because otherwise deleting `yarn.lock` from our repo will delete the file from the rest of team as well.

## Commands

```bash title:"Stop Tracking using .git/config/exclude"
# Stop Tracking using .git/config/exclude
git update-index --assume-unchanged yarn.lock
```

```bash title:"Add yarn.lock to .git/info/exclude"
# Add yarn.lock to your personal git exclude file
echo "yarn.lock" >> .git/info/exclude
```

```bash title: "Start Tracking using .git/config/exclude"
# Start Tracking using .git/config/exclude
git update-index --no-assume-unchanged yarn.lock
```


## Contents of `.git/info/exclude` 

