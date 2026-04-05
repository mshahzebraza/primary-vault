---
original_path: Notes/Tech Learning/OpenClaw/OpenClaw - useful commands.md
base: TechLearning
path_area: OpenClaw
categories:
- '[[TechLearning]]'
tags:
- open-claw
---
- how to check/update auth
- how to setup slack channel
- how to check pairing list


# Update Model Auth-Token/Api-Key

### Get Help
```bash
openclaw models -h


## Output

Usage: openclaw models auth [options] [command]
Manage model auth profiles

Options:
  --agent <id>          Agent id for auth order get/set/clear
  -h, --help            Display help for command

Commands:
  add                   Interactive auth helper (setup-token or paste token)
  login                 Run a provider plugin auth flow (OAuth/API key)
  login-github-copilot  Login to GitHub Copilot via GitHub device flow (TTY
                        required)
  order                 Manage per-agent auth profile order overrides
  paste-token           Paste a token into auth-profiles.json and update config
  setup-token           Run a provider CLI to create/sync a token (TTY
                        required)
```

### Get Help
```bash
openclaw models status

## Output
🦞 OpenClaw 2026.2.25 (4b5d4a4) — Meta wishes they shipped this fast.

Config        : ~/.openclaw/openclaw.json
Agent dir     : ~/.openclaw/agents/main/agent
Default       : openrouter/openrouter/auto (from openrouter/auto)
Fallbacks (0) : -
Image model   : -
Image fallbacks (0): -
Aliases (1)   : OpenRouter -> openrouter/auto
Configured models (1): openrouter/auto

Auth overview
Auth store    : ~/.openclaw/agents/main/agent/auth-profiles.json
Shell env     : off
Providers w/ OAuth/tokens (0): -
- openrouter effective=profiles:~/.openclaw/agents/main/agent/auth-profiles.json | profiles=1 (oauth=0, token=0, api_key=1) | openrouter:default=sk-or-v1...ee67a668

OAuth/token status
- none

```
### Setup Token/Key
If using `openrouter`, API Key should be used. So, 



```
openclaw onboard --auth-choice apiKey --token-provider openrouter --token "<OpenRouter API key from Proton Pass>"

```