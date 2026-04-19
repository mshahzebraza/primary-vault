---
type:
  - "[[Documentation]]"
categories:
  - "[[Work]]"
date: 2026-04-20
tags:
  - report
organization:
  - "[[aiquery.io]]"
projects:
  - "[[aq-client]]"
---

## Quick Summary

The dialog SQL editor opened too tall because its first size calculation happened too early.
At that instant, Monaco thought the editor was almost zero-width, so it overestimated how many visual lines were needed and returned a very large content height.
The app trusted that value and expanded the editor too much.

Fix: wait until layout is stable, then do the initial resize.

---

## What We Expected

- Editor starts at minimum height (`160px`) for short SQL
- Editor grows as content grows
- Editor stops growing at max (`500px`) and then scrolls

## What Actually Happened

1. User enters SQL in main Create Query form.
2. User opens Schedule/Save Preset dialog.
3. Dialog editor mounts with the prefilled SQL.
4. Editor appears too tall (sometimes near max).
5. First key press makes it snap back to normal.

Additional pattern that was observed:

- Shorter single-line SQL produced a smaller oversize.
- Longer single-line SQL produced a larger oversize.
- In simple terms, more words in the same line tended to increase the wrong initial height step-by-step.

---

## Plain-Language Explanation

The issue was not “missing content”.
The editor **did** have content (the prefilled SQL from the main form).

The real problem was **bad timing**:

- Monaco measured content height before dialog layout finished.
- During that moment, Monaco reported a broken width (very small / invalid).
- With broken width, Monaco treated one line as heavily wrapped and returned a big height.
- Auto-resize used that bad value.

When the user typed, Monaco measured again after layout stabilized, and height became correct.

Think of it like measuring text on a page before the page width is known:
if width is almost zero, every word looks like it needs a new line, so measured height looks huge.

---

## Walkthrough Example (Step by Step)

Use this simple input:

- SQL text: `select * from users`
- Expected initial height: `160px` (minimum)

What happened before the fix:

1. Dialog opens and Monaco mounts.
2. Monaco temporarily reports unstable width (`~5px` instead of real dialog width).
3. Monaco measures text as if it must wrap many times in a tiny width.
4. `getContentHeight()` becomes large (for example `260` or `374`).
5. Auto-resize applies that large value, so editor opens too tall.
6. User types one key.
7. By now, width is stable (`~615px`), so `getContentHeight()` becomes normal (`39`).
8. Auto-resize recalculates and returns to `160px`.

How input length affected the wrong initial height (before fix):

1. Input `test1` might open at height `x`.
2. Input `test1 test2` might open at height `x + y`.
3. Input `test1 test2 test3` might open at height `x + y + z`.

This is not because logical line count changed (it was still one line).  
It happened because the unstable tiny width caused Monaco to estimate extra wrapped visual lines.

What happens after the fix:

1. Dialog opens and Monaco mounts.
2. First-frame width is checked.
3. If width is unstable, initial resize is skipped.
4. Next frame runs when width is stable.
5. Height is calculated with correct width and editor starts at `160px`.

---

## Runtime Evidence (What Proved It)

During the failing dialog mount:

- Monaco layout width was unstable (`~5`)
- Monaco content width was invalid (`-5`)
- Measured content heights were large (`260`, `374`, `716`) for 1 logical line

A frame later:

- Width stabilized (`~615`)
- Content height became normal (`39`)

This exactly matched the visual behavior (oversized on mount, corrected on next interaction).

---

## Fix Applied

In the editor mount path (minimal mode):

1. If first-frame layout width/content width is unstable, skip initial resize.
2. Run a deferred resize on the next stable frame.

This keeps existing behavior intact:

- min/max constraints
- content-driven growth
- manual resize behavior

---

## Why It Sometimes Looked “More Expanded” for Longer SQL

With unstable near-zero width, longer one-line SQL is interpreted as more wrapped visual lines than shorter SQL.
So longer text produced a larger wrong initial height.

That is why `select a` could look less expanded than `select * from users`, even though both are one logical line.

---

## Why Width Was Unstable On First Measurement

Short answer: Monaco measured too early in the dialog mount lifecycle.

Longer explanation:

- The dialog and its inner layout (including scroll container/viewport sizing) were still settling in the first frame.
- Monaco’s initial measurement happened during that transient state, before parent width became final.
- In that transient pass, Monaco received an invalid/tiny effective width.
- On the very next frame, width became normal and stable.

So this was a timing/order-of-layout issue, not random behavior and not missing SQL content.

---

## Final Result

- Dialog editor now mounts at the correct height for short SQL.
- No big “snap down” on first keypress.
- Debug instrumentation has been removed.





![[Related Meetings.base]]
z