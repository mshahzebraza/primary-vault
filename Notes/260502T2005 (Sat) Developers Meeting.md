---
type: "[[Meeting]]"
categories:
  - "[[Meetings]]"
  - "[[Work]]"
date: 2026-05-02
tags:
  - journal
  - architecture
  - backend
organization:
  - "[[aiquery.io]]"
projects:
  - "[[aq-backend]]"
  - "[[aq-client]]"
attendees:
  - "[[Rajput]]"
---

## Context
> Brief note on why this meeting happened / what triggered it.

## Discussion

### Flow of TOTP
User signs in normally.  
User goes to **Security Settings**.  
1. User clicks **Enable authenticator app**.
2. Require password re-auth (Maybe)
3. Generate TOTP secret.
4. Show QR code(TOTP Url) + manual setup key.
5. User enters 6-digit code. (Might be different from the regular TOTPs)
6. Enroll factor. (should fail silently; on failure)
7. Show backup/recovery instructions.

**Login flow** 
1. User enters email/password.
2. Firebase returns MFA-required error.
3. App shows TOTP code input.
4. User enters code.
5. App resolves sign-in.
6. Continue to dashboard.

### Segration of Settings
- Account and Security Tabs of User Settings

## Decisions Made

## Action Items
- [ ] 