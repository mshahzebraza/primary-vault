---
original_path: Notes/Tech Learning/Misc/OpenCode.md
base: TechLearning
path_area: Misc
categories:
  - "[[TechLearning]]"
  - "[[Misc]]"
---
## Global MCP Setup

```bash
nano ~/.config/opencode/opencode.json
```

```json
{
  "$schema": "https://opencode.ai/config.json",
  "mcp": {
    "github": {
      "type": "local",
      "command": [
        "npx",
        "-y",
        "ghcr.io/github/github-mcp-server"
      ],
      "environment": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "YOUR_GITHUB_PAT" // Copy the token
      },
      "enabled": true
    }
  }
}
```

Note: For GitHub specifically, `opencode github install` can be used to setup a dedicated agent. But It'd need to request access to the repos/organizations.