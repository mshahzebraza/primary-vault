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

- [ ] Sync the unenroll logic of `src/client/views/settings/security-settings/security-settings.view.tsx` with the [Firebase Docs Link](https://firebase.google.com/docs/auth/web/totp-mfa#unenroll_from_totp_mfa) as the error code handled in docs is `auth/user-token-expired` vs the error code used in the code is `auth/requires-recent-login`. Confirm if we're using the correct code
- [ ] Investigate why did we receive this email
- [ ] Handle `revertMfa` mode in the Reset Password flow to branch out the resetPasswordFlow (Basic requirement is to show the - Contact Support for xyz... message)
- [ ] Create and show the revertMFA form
- [ ] Hide the Form for reversion behind Feature Flag. Otherwise show the message of contact support
- [ ] Refactor the optimize the Reset Password views and handle mode-based views
- [ ] Add a "Go back to Login" button/link on the Reset Password view
