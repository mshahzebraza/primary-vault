---
aliases:
- 🔐 How Does `req.user` Get Set in NestJS When Using Passport?
categories:
- '[[TechLearning]]'
tags:
- misc
---
**What confused me:**  
I never saw `validate()` being called but somehow `req.user.user_type` exists magically. How?

---

# ✨ The PassportJS Magic

1. You use `@UseGuards(AuthGuard('jwt'))`
2. That triggers Passport middleware under the hood
3. If JWT is valid:
   - Passport extracts payload
   - Calls `validate(payload)`
   - Whatever `validate()` returns gets assigned to `req.user`

---

# 🧠 Example

```ts
// some-jwt.strategy.ts
validate(payload: JwtPayload) {
  return {
    userId: payload.sub,
    email: payload.email,
    user_type: payload.user_type,
  };
}
```

```ts
// some.service.ts
@Get()
getProfile(@Req() req: Request) {
  console.log(req.user.user_type);
}

```

### Gotcha: 
The request object in the above example is not typed and getting it manually be accessing the object properties might cause bugs. A cleaner alternative includes typing it and accessing using a decorator.

---

### ✅ TL;DR

| Concept       | Explanation                                          |
| ------------- | ---------------------------------------------------- |
| `validate()`  | Called automatically by Passport when JWT is decoded |
| `req.user`    | Set to return value of `validate()`                  |
| Manual calls? | ❌ Never manually call `validate()`                   |




---
---

# 🔥🔥🔥🔥🔥THE LONG VERSION

# 💡 The Big Picture: What’s Happening?

When you use Passport.js inside NestJS, you're relying on:
- Nest’s `@nestjs/passport` wrapper
- One or more **strategies** (like JWT, Local, etc.)
- Middleware that **authenticates a request and injects a `user`** onto `req`
    

And here's the kicker...

> ⚡️ The `validate()` function in your strategy is _automagically called_ by Passport when it decodes and verifies the JWT (or other strategy logic).

---

# 🔍 1. Why does `validate()` work without being called?

Here’s the _deceptively simple truth_:

```ts
@Injectable()
export class JwtStrategy extends PassportStrategy(Strategy) {
  constructor() {
    super({
      jwtFromRequest: ExtractJwt.fromAuthHeaderAsBearerToken(),
      secretOrKey: 'topSecret', // Replace with config
    });
  }

  async validate(payload: any) {
    // This is AUTOMATICALLY CALLED by Passport if JWT is valid
    return {
      userId: payload.sub,
      email: payload.email,
      user_type: payload.user_type,
    };
  }
}

```


**What’s happening under the hood?**

- `PassportStrategy(Strategy)` sets up the JWT strategy with options
    
- When a request comes in with a Bearer token:
    
    - `Passport` extracts the token
        
    - Verifies it with your `secretOrKey`
        
    - Decodes the payload
        
    - Calls your `validate(payload)` method
        
- Whatever you return from `validate()` gets attached to `req.user`
    

So:

```ts
req.user = await validate(payload);
```

...is what's **implicitly happening**. You never see it, but it’s real.

---

# 🧙‍♂️ 2. What is `req.user` and how does it get there?

NestJS registers a **Passport middleware** behind the scenes when you use:

```ts
@UseGuards(AuthGuard('jwt'))
```


That `AuthGuard('jwt')`:
- Triggers Passport’s flow
- Authenticates the request
- Attaches the return value of `validate()` to `req.user`

So now inside your controller or service:

```ts
@Get('me')
@UseGuards(AuthGuard('jwt'))
getMe(@Req() req: Request) {
  console.log(req.user); // ← This is the object returned from `validate()`
}

```


---

# 🛡️ 3. But it doesn’t _validate_?

True… kind of 😅

`validate()` isn’t checking passwords or signing tokens. It’s just the final step of auth.

✅ It’s more about:

- Verifying user still exists (optional DB lookup)
    
- Returning useful info to be mounted on `req.user`
    
- Filtering out unwanted users (e.g. deactivated accounts)
    

So if you want to “reject” a user, you throw an exception:

```ts
async validate(payload: JwtPayload) {
  const user = await this.userRepo.findOne({ id: payload.sub });

  if (!user || user.banned) {
    throw new UnauthorizedException();
  }

  return user; // gets assigned to req.user
}

```

---

# 🧼 4. How to type `req.user` for IntelliSense?

This is 👑 if you're TypeScript lover (and I know you are).

Create your own interface for the user payload:

```ts
// auth/types/user-request.interface.ts
export interface AuthenticatedRequest extends Request {
  user: {
    userId: string;
    email: string;
    user_type: 'admin' | 'regular' | 'guest';
  };
}

```
Then in your controller or service:

```ts
import { AuthenticatedRequest } from './types/user-request.interface';

@Get('me')
getProfile(@Req() req: AuthenticatedRequest) {
  const userType = req.user.user_type; // 🔥 Fully typed
}
 
```

Or better yet, write a custom `@User()` decorator to extract and type just `req.user`:
```ts
// user.decorator.ts
export const User = createParamDecorator(
  (data: unknown, ctx: ExecutionContext) => {
    const request = ctx.switchToHttp().getRequest();
    return request.user;
  },
);

// Usage
@Get('me')
getProfile(@User() user: AuthUserPayload) {
  console.log(user.email); // 😍 Type-safe
}

```

---

# 🔥 TL;DR – Magic Explained

| Concept            | Explanation                                                                  |
| ------------------ | ---------------------------------------------------------------------------- |
| `validate()`       | Called by Passport _automatically_ after JWT is decoded                      |
| What it returns    | Gets attached to `req.user`                                                  |
| `AuthGuard('jwt')` | Hooks Passport into the request lifecycle                                    |
| Typing `req.user`  | Use `AuthenticatedRequest` interface or custom decorator                     |
| “Not validating”?  | You're expected to do DB checks or throw exceptions in `validate()` manually |

---
Related:
- [[Nest JS]]