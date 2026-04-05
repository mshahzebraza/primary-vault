---
categories:
- '[[TechLearning]]'
tags:
- misc
---
Here we discuss the JWT authentication setup in [[Nest JS]]. We'll discuss from the most basic (vanilla) approaches to then incrementally upgrade to using strategies from 3rd party libraries like postman.

## Level 1

### General Flow
#### Authentication/Login
- On login, backend validates credentials
- If correct, a token is sent to client
- On each request to a protected resource, the token must be sent.
- Backend verifies the token, and returns the requested resource if valid token received.
#### Resource Protection
- A guard is employed that checks the Auth Header for the bearer token
- If the bearer-token is verified, the decoded data can be used to attach info to request object
#### Refresh Token/Logout
...
### High Level Implementation
#### Resources
1. `UsersModule`
	1. `UsersService`
		1. `findUserByEmail`/`findUserByUsername`
2. `AuthModule`
	1. `AuthController`
		1. `/login` endpoint
	2. `AuthService`
		1. `validateUser`
		2. `login`
	3. `AuthGuard`
		1. `canActivate`
#### Step by Step Code Traversal
##### Authentication/Login
- `AuthController` listens to `/login` endpoint and calls the `AuthService.login` 
- `AuthService.login` calls the
	- `AuthService.validateAndGetUserInfo` 
		- `UsersService.findUserByEmail` (gets the user and compares the received password with stored `hash`)
		- removes the sensitive information before returning user data
	- `AuthService.prepareToken`
		- prepares the token payload from user-info as per JWT standards
		- uses `JWTService.generateToken`/`JWTService.sign` to tokenize the payload
		- return token
	- returns the token and brief user info
##### Resource Protection
- `ProtectedResource` listens to `/me` endpoint but is decorated with using `UseGuard(AuthGuard)`
- `AuthGuard` uses a standard `canActivate` method which returns a Boolean to allow/disallow access to the guarded resource
	- First it extracts the Bearer Token from Authorization Header using the context
	- Verifies the Bearer Token and attaches the data to request object
##### Refresh Token/Logout
...


## Level 2: Using Passport JS
### General Flow
The flow is mostly similar to the previous Authentication Flow. 

### High Level Implementation
#### Resources
1. `LocalAuthStrategy` this will serve as the authentication/login service but we don't handle the logic for generating token 
2. `LocalAuthGuard` this will depend on the `LocalAuthStategy`
#### Step by Step Code Traversal
##### Authentication/Login
- `AuthController` listens to `/login` endpoint and calls the `AuthService.login` 