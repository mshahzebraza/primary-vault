---
aliases:
- OpenClaw/Clawdbot Setup
categories:
- '[[TechLearning]]'
tags:
- open-claw
---
**Reference:** [ClawdBot - Full Tutorial & Setup Guide (SECURE)](!https://www.youtube.com/watch?v=tnsrnsy_Lus)
- VPS Provider: KVM2
## TailScale VPN Setup:
To limit connection through auth networks when VPN is on


```
Public key
nodekey:e07ce0e03dd58a4efca68ad784a35a1480420af72d031ea1a1c06922a93c7f2b
Hostname
srv1349367
Operating system
linux (6.12.63+deb13-amd64)
Tailscale version
1.94.1-t62c6f1cd7-g09fea6572
```
- Signup
- Allow Personal Device to Connect to VPS
- Test Connection through admin account via ping command
- Test the `tailscale status`

## SSH Config
Instead of connecting to VPS through its IP, setup connection through tailwind IP
- update SSH config
	- `nano /etc/ssh/sshd_config`
	- disallow root password login
	- change listen-address to Tailscale IP
- add new user: `mshahzebraza`: `p44 (full)`
- give admin access to new user:  `usermod -aG sudo mshahzebraza`
- switch user (to new user): `su - mshahzebraza`
- run `sudo whoami`; Expected output `root`
- logout `logout` (logs out to the root user)
- restart ssh: `system restart ssh`
- logout `logout`; exits out of the ssh

After all these commands, SSH connection attempt through root user wouldn't be successful. We've secured the network access through the tailscale only

## OpenClaw Installation

- change the OS to the VPS OS and copy the one-liner command
`curl -fsSL https://openclaw.ai/install.sh | bash`
- add the API key (recommended by Tim is `claude`/`openapi`)
- keep other option the same and use the gateway bind of loopback and config
```
◇  I understand this is powerful and inherently risky. Continue?
│  Yes
│
◇  Onboarding mode
│  Manual
│
◇  What do you want to set up?
│  Local gateway (this machine)
│
◇  Workspace directory
│  /home/mshahzebraza/.openclaw/workspace
│
◇  Model/auth provider
│  Google
│
◇  Google auth method
│  Google Gemini API key
│
◇  Enter Gemini API key
│  [Google Gemini API key stored in Proton Pass — not in repo]
│
◇  Model configured ─────────────────────────────────╮
│                                                    │
│  Default model set to google/gemini-3-pro-preview  │
│                                                    │
├────────────────────────────────────────────────────╯
│
◇  Default model
│  google/gemini-2.5-flash-lite
│
◇  Gateway port
│  18789
│
◇  Gateway bind
│  Loopback (127.0.0.1)
│
◇  Gateway auth
│  Token
│
◇  Tailscale exposure
│  Off
│
◇  Gateway token (blank to generate)
│
│
◇  Channel status ────────────────────────────╮
│                                             │
│  Telegram: not configured                   │
│  WhatsApp: not configured                   │
│  Discord: not configured                    │
│  Google Chat: not configured                │
│  Slack: not configured                      │
│  Signal: not configured                     │
│  iMessage: not configured                   │
│  Feishu: install plugin to enable           │
│  Google Chat: install plugin to enable      │
│  Nostr: install plugin to enable            │
│  Microsoft Teams: install plugin to enable  │
│  Mattermost: install plugin to enable       │
│  Nextcloud Talk: install plugin to enable   │
│  Matrix: install plugin to enable           │
│  BlueBubbles: install plugin to enable      │
│  LINE: install plugin to enable             │
│  Zalo: install plugin to enable             │
│  Zalo Personal: install plugin to enable    │
│  Tlon: install plugin to enable             │
│                                             │
├─────────────────────────────────────────────╯
│
◇  Configure chat channels now?
│  Yes
```

