---
type: "[[Task]]"
categories:
  - "[[Work]]"
  - "[[Tasks]]"
organization: "[[aiquery.io]]"
projects:
  - "[[aq-client]]"
status: active
priority: P1
date: 2026-07-09
has-enhancements: false
related-tasks:
  - "[[260709 Ask Fleet aka AI Investigation UI Review and Backend Integration Meeting]]"
---

## Overview
Ask Fleet (aka AI Assistance / "Ask the Fleet") is a natural-language query feature: the user asks a question about the fleet, it's translated into an aggregate SQL query, run across the selected agents, and returned as a virtualized results table. The UI was built from a Claude-generated MVP artifact handed over by backend eng/tech lead Rajput; the backend itself isn't built yet. [[260709 Ask Fleet aka AI Investigation UI Review and Backend Integration Meeting|This meeting]] was a UI review with Rajput plus a working session to pin down the backend integration contract.

## Current Tasks
- [ ] Add a touch of brand purple to the Ask Fleet UI (brand color = purple shade, decided [[260623 Weekly Scrum - UI Updates, Tags|2026-06-23]])
- [ ] Remove the total-agents count from the response summary — no backend support
- [ ] Remove the AI investigation summary shown per message — no backend support
- [ ] Replace the percentage/phase progress bar with a front-end-only fake version — no streaming endpoint exists for real progress
- [ ] Reposition New Session and History actions to the top right
- [ ] De-enterprise the look — remove the separator line under the header

## Backend Integration Flow
Agreed with Rajput during the UI review. Three sub-flows: **New Session**, **Session Comeback**, and **History**.

### New Session
1. `POST v2/ask-fleet` creates the session — payload: `agent-groups`, `ask_prompt`.
   - Backend responds with the session as pending/success; message aggregation is still pending at this point.
   - Client redirects to the session view and starts subscribing to the message stream.
2. **Message stream** (session's first/only message at this point): while streaming, show only a skeleton — nothing else.
   - On a `success` status from this stream, two things come back: the **aggregate SQL query** and **suggestions** (kept in memory, not persisted).
3. Once the message stream succeeds, subscribe to the **query-response-result stream**. This reports the breakdown of how many targets/hosts have responded.
4. As soon as there's a workable increase in responded targets, `POST` the **aggregated-SQL-search** endpoint using the aggregate SQL query from step 2. Its result populates the virtualized response table.
5. Any follow-up question in the same session repeats steps 2–4: create message → subscribe to message stream → subscribe to query-response stream → aggregated-SQL-search.

### Session Comeback
Returning to a session already in progress:
1. `GET` session info.
2. `GET` all messages in the session.
3. Past messages are shown as metadata only — none of their result data is kept in memory (it can be large).
4. Only the **latest** message's status is checked to decide what to resume:
   - Message not yet created → open the message stream.
   - Message created, result pending → open the query-response-result stream.
   - Once query response is available → `POST` aggregated-SQL-search as in the New Session flow.

### History
Two tabs:
- **Recents**
  - Section 1: the single most recent session, with its messages shown accordion-style.
  - Section 2: the most recent questions across all sessions.
- **Sessions**
  - Flat list of session info only — not expandable, no drill-in to individual questions/messages.

## Decisions
- Brand color accent (purple) applied to Ask Fleet — consistent with the app-wide brand color decision.
- AI investigation summary per message is cut from MVP scope — backend does not support it.
- Progress bar during message creation is a front-end-only simulated animation — no real progress-streaming endpoint is planned.
- New Session, Session Comeback, and History flows above are the agreed contract shape for backend integration.

## Enhancements
- loading statuss should continue even when first respones is fetched but rest is pending howvever the color of status dot can change. to blue/orange etc. or maybe with a status dot of green inside the loader. ![[loading statuss should continue even when first respones.png]]
- Refactor the panels and message components in the `ask-fleet-session.view.tsx`
- 

![[Related Bugs.base]]

![[Related Meetings.base]]
