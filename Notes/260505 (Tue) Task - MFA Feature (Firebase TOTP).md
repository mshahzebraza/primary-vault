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

Adds TOTP-based two-factor authentication via Firebase. Users enroll an authenticator app (Google Authenticator, Authy, etc.) from **Settings → Security**. Once enrolled, every sign-in requires a password and a 6-digit TOTP code. Users can disable MFA at any time, with identity re-verified first. The tenant owner can monitor enrollment status across the team but cannot enforce it.

The Security tab is gated behind the `totp_mfa` feature flag (default off) so it can be enabled per-environment when ready.

## Business Requirements

- **Optional Enrollment:** MFA is opt-in; users choose whether to configure it.
- **User Visibility:** Users can see their own MFA status on the Security settings page.
- **Owner Visibility:** The tenant owner can view the MFA enrollment status of all users in the tenant.
- **No Enforcement:** Owners cannot force-enable MFA for other users.

## Technical Design

### TOTP Enrollment Flow

Triggered from **Settings → Security tab**:

1. Email verification is enforced before enrollment can begin (client-side + Firebase).
2. User clicks **Enable MFA**.
3. A side-by-side dialog shows a QR code (TOTP URL) and the raw manual setup key.
4. User scans the QR (or enters the key manually) in their authenticator app.
5. User enters the 6-digit OTP to confirm enrollment.
6. On success: toggle shows "Enabled". On failure: silent retry — a fresh QR is regenerated if the session has expired (~10 min timeout).

### Login Challenge Flow

**Scenario B applies** — the app owns the challenge UI:

1. User enters email + password.
2. Firebase returns an `MFA required` error.
3. App shows a TOTP code input step (instead of redirecting to the dashboard).
4. User enters the 6-digit code.
5. App resolves the sign-in with Firebase.
6. Redirect to dashboard. Wrong/expired code shows an inline error; the OTP step stays for retry.

### Re-authentication Flow

Sensitive operations (enabling/disabling MFA) gate on session freshness:

- If the session is stale, a re-auth modal appears automatically.
- For users with MFA enrolled, the modal transitions inline from a password step to an OTP step — no separate screen.
- The `getIsFreshAuth()` synchronous getter was exported from the auth store to fix a bug where the stale mount-time value of `useIsFreshAuth()` could skip the re-auth gate after 30+ minutes on the page.

### Backend Sync

On enrollment and unenrollment, a best-effort POST is sent to `/auth/mfa/enable` and `/auth/mfa/disable` to keep the backend `mfaEnabled` flag in sync. Failures are silent — Firebase is the source of truth.

## Tasks

### Research

- [x] Watch tutorials on Firebase Authentication + TOTP setup (Google Authenticator, Authy).
- [x] Resolved **Scenario A vs B**: Firebase does **not** handle the challenge UI natively — the app must build custom views (Scenario B).

### UI

- [x] **Security Tab — Settings Page:** MFA configuration screen (gated by `totp_mfa` flag) with status toggle, QR enrollment dialog, and disable flow.
- [x] **MFA Challenge Screen — Login Flow:** Custom TOTP input step after password sign-in for enrolled users.
- [x] **Re-auth Modal:** Extended to handle MFA-enrolled users inline (password → OTP steps).
- [ ] *(Nice-to-have)* **Team Settings Page:** Read-only MFA status indicator per user for the tenant owner.

![[Related Meetings.base]]
