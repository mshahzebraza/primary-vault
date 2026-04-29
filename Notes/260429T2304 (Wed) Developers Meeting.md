---
type: "[[Meeting]]"
categories:
  - "[[Meetings]]"
  - "[[Work]]"
date: 2026-04-29
tags:
  - scrum
organization:
  - "[[aiquery.io]]"
projects:
  - "[[aq-client]]"
attendees:
  - "[[Rajput]]"
---
## Context
- clickhouse invitation received in gmail. Need to accept
- MFA

## MFA
### 1. Business Logic & User Requirements

- **Optional Enrollment:** MFA will be optional for all users; they can choose whether or not to configure it.
- **Visibility & Status:**
    - **User Level:** Users can view their own MFA configuration status on their profile/security page.
    - **Admin/Owner Level:** The tenant owner (root account) can monitor the MFA status of all users within the tenant.
- **No Enforcement:** While owners can view the status, they currently lack the authority to force a user to enable MFA.

### 2. MFA Registration Flow

The setup process occurs within the application after the user has logged in:

1. **Navigation:** User navigates to the **Security** tab/page.
2. **Trigger:** User clicks the **Setup MFA** button.
3. **Registration UI:** A pop-up window (likely a Firebase-managed interface) will appear.
4. **Methods:** Users will be offered two standard registration options:
    - **QR Code** scanning for authenticator apps.
    - **Manual Code** entry.
5. **Provider:** Firebase is the primary provider for handling the registration and storage of MFA metadata.

### 3. Authentication & Verification Flow

Once configured, the login sequence will be updated to include a second factor:

- **Verification:** Subsequent sign-ins will require an MFA code from a standard authenticator tool.
    
- **Backend Handling:** Firebase will manage the actual verification of the token.
    

### 4. Implementation Considerations & Technical Debt

There is a specific technical uncertainty regarding the **Subsequent Sign-in** user experience:

- **Scenario A (Automatic):** Firebase handles the redirection to an MFA input screen and returns the user to the application's callback URL upon success.
- **Scenario B (Manual):** The application must intercept the initial login response. If Firebase indicates MFA is required, the application must manually trigger a custom "MFA Token Input" view.

> **Next Step:** Verify the Firebase Authentication documentation to determine if the MFA challenge UI is handled natively or requires a custom-built view in the frontend.