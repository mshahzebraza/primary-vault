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
date: 2026-05-05
tags:
  - mfa
  - auth
  - firebase
---

## Overview

Add optional Multi-Factor Authentication (TOTP) via Firebase to the app. Users enroll through a new Security tab in Settings; enrolled users are challenged for a TOTP code on every subsequent login. The tenant owner can monitor enrollment status across the team but cannot enforce it.

## Business Requirements

- **Optional Enrollment:** MFA is opt-in; users choose whether to configure it.
- **User Visibility:** Users can see their own MFA status on the Security settings page.
- **Owner Visibility:** The tenant owner can view the MFA enrollment status of all users in the tenant.
- **No Enforcement:** Owners cannot force-enable MFA for other users.

## Technical Design

### TOTP Enrollment Flow

Triggered from **Settings → Security tab**:

1. User clicks **Enable authenticator app**.
2. *(Maybe)* Require password re-authentication.
3. Generate TOTP secret.
4. Display QR code (TOTP URL) and manual setup key.
5. User enters the 6-digit verification code.
6. Enroll the factor — fail silently on error (surface a retry prompt).
7. Show backup / recovery instructions.

### Login Challenge Flow

Triggered automatically when an enrolled user signs in:

1. User enters email + password.
2. Firebase returns an `MFA required` error.
3. App displays TOTP code input screen.
4. User enters the 6-digit code.
5. App resolves the sign-in with Firebase.
6. Redirect to dashboard.

### Open Question — Challenge UI Ownership

There is an unresolved question about who renders the MFA challenge screen:

- **Scenario A (Automatic):** Firebase handles the redirect to an MFA input screen and returns the user to the app callback on success — no custom UI needed.
- **Scenario B (Manual):** The app must detect the `MFA required` signal from Firebase and render a custom TOTP input view before completing sign-in.

## Tasks

### Research

- [ ] Watch tutorials on Firebase Authentication + TOTP setup (Google Authenticator, Authy).
- [ ] Review Firebase docs to resolve **Scenario A vs B** — does Firebase handle the challenge UI natively, or must the app build a custom view?

### UI

- [ ] **Security Tab — Settings Page:** MFA configuration screen showing current status (enabled / disabled) and the setup trigger button.
- [ ] **MFA Challenge Screen — Login Flow:** Custom TOTP input screen shown after the Firebase `MFA required` signal *(needed only if Scenario B applies)*.
- [ ] *(Nice-to-have)* **Team Settings Page:** Read-only MFA status indicator per user for the tenant owner.

![[Related Meetings.base]]
