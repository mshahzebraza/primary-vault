---
type: "[[Task]]"
categories:
  - "[[Work]]"
  - "[[Tasks]]"
date: 2026-06-24
tags:
  - feature
  - ux
organization: "[[aiquery.io]]"
projects:
  - "[[aq-client]]"
status: active
priority: P2
---

## Overview
Add `Ctrl+Enter` keyboard shortcut to submit active query from the SQL editor (rapid response editor). Currently users must click the submit button even when focus is in the editor. Pair with a subtle hover hint that appears after a second of inactivity — visible only when a callback is provided, and configurable with a sensible default label.

## Current Tasks
- [ ] Accept an optional `onCtrlEnter` callback prop in the SQL editor component
- [ ] Always listen for `Ctrl+Enter` keydown when callback is present (no waiting)
- [ ] Track inactivity on the editor (1s debounce); show hover hint only after inactivity
- [ ] Position hint absolutely at bottom-right of editor, subtle styling
- [ ] Only render hint if `onCtrlEnter` callback is passed
- [ ] Hint text configurable with a short generic default (e.g. "Press Ctrl+Enter to submit")
- [ ] Wire callback in rapid response editor view

## Spec (original prompt)
> Also, is it possible to change the SQL editor component in a way that it allows a callback to be used for the control enter key press? I'm asking this because when on an input field, we press enter, it automatically submits the form. However, for the SQL editor, we have to use the mouse, even when we are in the editor and we have typed our entry. We can't just control enter and expect it to work as a submit call. We necessarily have to use a mouse currently. So, is there a solution to that where we show a hovering hint to the user, absolutely positioned on the bottom right of the SQL editor, and only visible with subtle styles when it is detected that the user has stopped typing for, let's say, a second? So it's only when the user has stopped typing for a second that we show the hint. But the functionality to control enter should always be listening so that a user who already knows how the control enter functionality works can use it without waiting on the hint. But for new users, the hint would help them. If the system detects inactivity for the SQL editor, they can prompt the user to click control enter to submit the text, or something. And, of course, this hint should only be visible if the callback is passed, and this hint should also be configurable with a default value which is generic and short.
