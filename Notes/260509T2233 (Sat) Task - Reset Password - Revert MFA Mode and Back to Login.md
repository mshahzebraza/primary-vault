---
type: "[[Task]]"
categories:
  - "[[Work]]"
  - "[[Tasks]]"
organization:
  - "[[aiquery.io]]"
projects:
  - "[[aq-client]]"
status: active
priority: P2
date: 2026-05-09
tags:
  - reset-password
  - mfa
  - auth
---

## Overview

Two UX gaps in the Reset Password flow: it does not currently handle the `revertMfa` mode (entered when a user needs to reset their MFA as part of the password reset journey), and there is no "Back to Login" navigation affordance on the reset password view.

## Current Tasks

- [ ] Handle `revertMfa` mode in the Reset Password flow
- [ ] Add a "Go back to Login" button/link on the Reset Password view
