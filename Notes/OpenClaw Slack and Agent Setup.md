---
categories:
- '[[TechLearning]]'
tags:
- open-claw
---
`[OpenRouter key — stored in Proton Pass]`

Slack Communication was investigated using follows.
`openclaw logs`
revealed that same permission error was causing no reply to be received even after pairing.
```
01:11:11 error gateway/channels/slack {"subsystem":"gateway/channels/slack"} slack final reply failed: Error: An API error occurred: missing_scope
```
google search revealed that in addition to `chats:write` and `im:write` is required for enabling the DM permission for the both. The permission was updated and the bot was reinstalled, after which the pairing had to be done again and the replies from openclaw were received in dm.
However, now we had some API error.
```
01:11:10 error diagnostic {"subsystem":"diagnostic"} lane task error: lane=session:agent:dev:slack:direct:u0agu1rn59d durationMs=6 error="Error: No API key found for provider "anthropic". Auth store: /home/clawadmin/.openclaw/agents/dev/agent/auth-profiles.json (agentDir: /home/clawadmin/.openclaw/agents/dev/agent). Configure auth for this agent (openclaw agents add <id>) or copy auth-profiles.json from the main agentDir."
```
it was observed that due to some previous config reset or manual editing of the `openclaw.json` file, the main agent profile may have been replaced by another agent `dev` and that didn't have any auth profiles set up.
Now the `openclaw agents list` showed only the `dev` agent listed. However, 
It was also found that the `main` agent also didn't have anything meaningful stored in its file i.e. ``