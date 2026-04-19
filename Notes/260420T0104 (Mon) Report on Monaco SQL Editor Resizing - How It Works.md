---
type:
  - "[[Documentation]]"
categories:
  - "[[Personal]]"
  - "[[Work]]"
date: 2026-04-20
tags:
  - journal
  - report
organization:
  - "[[aiquery.io]]"
projects:
  - "[[aq-client]]"
---
## Why this report exists
This report explains the current resizing behavior of the Monaco SQL editor in plain language, with enough technical depth for implementation and review discussions.
It covers:
- how resizing is wired,
- normal and edge-case walkthroughs,
- why `requestAnimationFrame` is used,
- whether this `requestAnimationFrame` usage is safe and recommended.

---

## Architecture map (which part does what)
### 1) `BaseMonacoEditor` (`src/components/monaco-editor/monaco-editor-base.tsx`)
This is the orchestrator:
- renders the wrapper whose `height`, `minHeight`, and `maxHeight` are controlled in minimal mode,
- creates refs for editor instance + wrapper,
- connects `useEditorAutoResize` and `useEditorMount`,
- passes Monaco mount callback and value change callback into the Monaco component.
Think of it as the coordinator, not the calculator.
### 2) `useEditorAutoResize` (`src/components/monaco-editor/hooks/use-editor-auto-resize.ts`)
This is the height engine:
- stores current editor height state,
- computes new height from content and constraints,
- detects manual drag resize via `ResizeObserver`,
- keeps a manual-resize floor so auto-resize does not shrink below user drag height.
### 3) `useEditorMount` (`src/components/monaco-editor/hooks/use-editor-mount.ts`)
This is mount-time control:
- handles focus/blur registration,
- triggers initial resize attempts after mount,
- guards against unstable first-frame layout width,
- performs deferred resize on a later frame once layout is stable,
- subscribes to Monaco content changes to resize on typing.
### 4) Constants and options
- `src/components/monaco-editor/constants/editor.constants.ts`
  - minimal mode min/max heights: `160` / `500`
  - thresholds used for manual/programmatic resize detection
- `src/components/monaco-editor/utils/editor-options.ts`
  - `wordWrap: 'on'` (important for content height behavior)
  - `automaticLayout: true` (Monaco reacts to container size changes)

---

## Core resizing logic in one sentence
In minimal mode, height is:
`min(MAX_HEIGHT, max(MIN_HEIGHT, contentHeight, manualHeightFloor))`
So the editor:
- never goes below minimum,
- never exceeds maximum,
- respects user drag height floor,
- grows with content when needed.

---

## Walkthrough examples
### A) Normal case: short SQL in main form
Example input: `select 1;`
1. Editor mounts.
2. Layout stabilizes quickly.
3. Mount resize computes small `contentHeight`.
4. Clamp returns minimum `160`.
5. Editor starts at `160px`.
Result: expected behavior.

---

### B) Normal case: user types multiple lines
Example input grows to:
```sql
select * from users;
select * from processes;
select * from os_version;
```
1. Monaco content-change listener fires on each edit.
2. `updateEditorHeight()` recomputes `contentHeight`.
3. Height grows stepwise until max `500`.
4. Beyond max, wrapper stays at `500` and Monaco scrolls.
Result: expected growth and cap.

---

### C) Edge case (historical bug): dialog mount with prefilled SQL
Before the fix:
1. Dialog opens.
2. Monaco measures too early (first frame).
3. Width is temporarily unstable/tiny.
4. With `wordWrap: 'on'`, Monaco overestimates visual wrapped lines.
5. `contentHeight` becomes very large.
6. Auto-resize trusts this and editor opens too tall.
7. First keypress triggers new measurement after layout settles.
8. Height snaps back down.
After the fix:
9. First frame checks layout width.
10. If width is unstable, early resize is skipped.
11. Deferred resize runs on later frame.
12. Width is stable, `contentHeight` is correct.
13. Editor starts at expected height.
Result: no oversized initial mount.

---

### D) Manual drag-resize behavior
1. User drags editor wrapper taller.
2. `ResizeObserver` sees observed height differs from last programmatic height.
3. Hook marks it as manual resize and stores new manual floor.
4. Later content shrink does not reduce height below that floor.
Result: user drag intent is preserved.

---

### E) Full mode behavior
In full mode, minimal auto-resize path is bypassed. Full mode uses different sizing constraints and is not part of the minimal auto-resize engine.
Result: minimal-mode resizing rules do not interfere with full mode.

---

## `requestAnimationFrame (rAF)`
### What is `requestAnimationFrame (rAF)`?
`rAF` means `requestAnimationFrame`.
It’s a browser API used to run a callback right before the next screen paint/frame render.  
In simple terms: “run this on the next visual frame when layout is more up-to-date.”
Common use cases:
- smooth animations,
- reading/updating layout at the right time,
- avoiding measuring DOM too early during transient render states.
### Why `requestAnimationFrame` is used here
`requestAnimationFrame` (rAF) schedules code to run right before the browser paints the next frame.
In UI/layout code, this helps when you need **post-layout, frame-aligned measurements** instead of immediate synchronous reads during transient render phases.

---

### rAF usage in this codebase (current)
#### 1) In `useEditorMount`: first-frame guarded resize
- rAF waits one frame after mount.
- code checks if width is stable.
- if unstable, it skips immediate resize.
Why: avoid incorrect first-frame measurements in dialog mount timing.
#### 2) In `useEditorMount`: nested rAF deferred resize
- second resize attempt runs one more frame later.
- by then, dialog/container layout is usually stable.
Why: ensure at least one stable-frame resize for prefilled content.
#### 3) In `useEditorAutoResize`: after height update, call `editor.layout()` inside rAF
- height state update is applied,
- then Monaco layout is requested in next frame.
Why: keep Monaco internal viewport in sync with wrapper size after React state update.
#### 4) In manual resize path: `editor.layout()` also inside rAF
Why: same reason as above, but for user-dragged size changes.

---

## Is this an antipattern?
Short answer: **No, not by itself.**
Using rAF for layout-sensitive UI code is a common and valid pattern.
It becomes problematic when:
- used as a blind “fix everything” delay with no condition,
- chained repeatedly without clear stop criteria,
- used where deterministic event hooks/lifecycle guarantees would be cleaner.
In this implementation:
- rAF usage is targeted to measurement/layout synchronization,
- unstable-width guard is explicit and deterministic,
- no unbounded loops are used.
So this is **reasonable and safe** for this problem.

---

## Is it required here?
For this specific bug class (first-frame invalid dialog width), some deferred measurement mechanism is required.
Could you do it without rAF?
- sometimes yes (e.g., stronger “ready” signal from parent dialog layout),
- but with third-party editor + modal timing, rAF is often the most practical and robust option.
Given current architecture, rAF is justified.

---

## Is it safe to use in production?
Yes, in this form:
- no busy loops,
- small bounded number of calls,
- frame-aligned scheduling,
- no blocking work inside callbacks.
Performance risk is low for this implementation.

---

## Practical recommendations (if refactoring later)
If you want to simplify further in future:
1. centralize mount-time “stable layout check + deferred retry” in one utility,
2. keep one clearly named mount-resize strategy function,
3. document why nested rAF exists (dialog/transient layout stabilization),
4. add a regression test for “prefilled dialog SQL mounts at min height”.

---

## Final takeaways
- Resizing engine is structurally sound: min/max clamps + manual floor + content growth.
- The historical bug was a timing/measurement issue, not formula logic.
- rAF usage here is appropriate for layout synchronization and is not an antipattern in this context.