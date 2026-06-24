---
type: "[[Meeting]]"
categories:
  - "[[Meetings]]"
  - "[[Work]]"
date: 2026-04-15
tags:
  - journal
organization:
  - "[[scholarbee]]"
projects:
  - "[[aq-backend]]"
attendees:
  - "[[M. Arsalan]]"
  - "[[Aliza Sabahat]]"
---

## Context
> On the request of Mr. Haroon and Mr. Usman, signup flow needs to be simplified
## Discussion
- signup will replace first name and last name with full name
- applications will still accept both names, but keep last name optional

## Action Items
- [x] first name + last name -> fullname in user schema
- [x] [[#make application credentials accept optional lastname]]
- [x] [[#Documents + toc validation removal]]
- [x] auto signup by sending tokens on signup
- [x] update all documentation
- [x] create the full name of existing users as well
- [x] [[#Testing|Testing of all flows]]


### make application credentials accept optional lastname
- updated application snapshot to require first and last name from user
	- **Problem:** user might not already have the 2 fields. 
		- Option 1: If we decide to accept it in application DTO, then user might input information each time differently. 
		- **Option 2:** Otherwise, we can prompt the user to save first name and last name in the profile completion on frontend, if not already completed. This is appropriate UX because we already show the steps for profile completion at the time of application
### Documents + toc validation removal
- removed from dto and schema
- deprecate the code for validation and add todo to use it in guard level validation instead of in service methods


## Create Full Name for existing users
Run the following command in mongosh
```sh
db.users.updateMany(
  {}, 
  [
    {
      $set: {
        full_name: {
          $trim: {
            input: {
              $concat: [
                { $trim: { input: { $ifNull: ["$first_name", ""] } } },
                " ",
                { $trim: { input: { $ifNull: ["$last_name", ""] } } }
              ]
            }
          }
        }
      }
    }
  ]
)
```

## Testing
- [x] signup without legal docs
- [x] signup with fullname
- [x] apply without fullname
- [x] apply with fullname
- [x] apply without toc
- Auto signup (without logging in)
	1. Call `POST /auth/signup` with valid payload → response should contain `accessToken`, `refreshToken`, and `user`
	2. Use the returned `accessToken` as `Bearer` on a protected endpoint → should succeed
	3. Call `POST /auth/refresh` with the returned `refreshToken` → should return new token pair
	4. Call `POST /auth/login` with same credentials after signup → should still work (refresh token hash gets overwritten, which is acceptable)
	5. Check DB: user document should have a non-null `refreshTokenHash` immediately after signup