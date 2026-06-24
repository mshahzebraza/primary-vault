---
type: "[[Task]]"
categories:
  - "[[Work]]"
  - "[[Tasks]]"
organization:
  - "[[aiquery.io]]"
projects:
  - "[[aq-client]]"
status:
  - completed
priority: P2
date: 2026-05-09
tags:
  - mfa
  - auth
---

## Overview

Two UX gaps in the Reset Password flow: it does not currently handle the `revertMfa` mode (entered when a user needs to reset their MFA as part of the password reset journey), and there is no "Back to Login" navigation affordance on the reset password view.

## Current Tasks

- [x] Sync the unenroll logic of `src/client/views/settings/security-settings/security-settings.view.tsx` with the [Firebase Docs Link](https://firebase.google.com/docs/auth/web/totp-mfa#unenroll_from_totp_mfa) as the error code handled in docs is `auth/user-token-expired` vs the error code used in the code is `auth/requires-recent-login`. Confirm if we're using the correct code
- [x] Investigate why did we receive this email
- [x] Handle `revertMfa` mode in the Reset Password flow to branch out the resetPasswordFlow (Basic requirement is to show the - Contact Support for xyz... message)
- [x] Create and show the revertMFA form
- [x] Hide the Form for reversion behind Feature Flag. Otherwise show the message of contact support
- [x] Refactor the optimize the Reset Password views and handle mode-based views
- [x] Add a "Go back to Login" button/link on the Reset Password view
