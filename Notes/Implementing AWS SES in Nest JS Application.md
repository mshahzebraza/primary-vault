---
status: completed
tags:
- devops
- RnD
original_path: Notes/Work/aiquery.io/R&D/Implementing AWS SES in Nest JS Application.md
base: Work
organization: '[[aiquery.io]]'
path_area: R&D
categories:
- '[[Work]]'
- '[[aiquery.io]]'
---

## Overview
Integrate AWS SES into the NestJS backend of aiquery.io to replace the existing nodemailer setup.

## Setup Steps

### AWS Console
1. Add SES identities (domain + email)
2. Verify both domain and email identities
3. Store SMTP credentials generated from AWS SES Settings

### Code
1. Use the AWS SDK for SES (not nodemailer)
2. Ensure the role/user running the application has `ses:SendEmail` permission
3. Run `ListIdentities` command before sending to confirm identity is verified

## Challenges & Fixes

**"Incorrect Credentials" or "Multiple credential sources detected"**
- Ensure the server's IAM user/role has SES send permissions
- Ensure `ListIdentities` runs before sending
- If multiple credentials persist, unset duplicate AWS env vars in shell — don't have both `AWS_PROFILE` and `AWS_ACCESS_KEY_ID`/`AWS_SECRET_ACCESS_KEY` set simultaneously

**"Email address is not verified" error**
- In SES Sandbox mode, both TO and FROM addresses must be verified
- Fix: Use literal `US-EAST-1` (all caps) instead of `us-east-1` for the region string

## Related Notes
- [[Nest JS]]
- [[Tasks Manifest - Ai Query]]
