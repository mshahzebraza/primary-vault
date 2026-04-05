---
categories:
- '[[TechLearning]]'
tags:
- misc
---

  
## 🐞 The Problem

I had a custom AuthGuard (`AuthV1Guard`) that needed to use my `AuthService` to validate JWT tokens. I injected `AuthService` into the guard like this:

```ts
export class AuthV1Guard implements CanActivate {
    constructor(private authService: AuthService) {}
    // ...
}
```

But when I hit a protected route, I got this error:

```
TypeError: Cannot read properties of undefined (reading 'validateToken_v1')
```

## 🤔 Why Did This Happen?

- I thought only the **service** (`AuthService`) needed `@Injectable()`, since it's being injected.
- But the **guard** (`AuthV1Guard`) is the **consumer** — it receives the dependency.
- **Without `@Injectable()` on the guard, NestJS does NOT use its dependency injection system to create it.**
- So, `this.authService` was `undefined` inside the guard.

## 💡 The Solution

Add `@Injectable()` to the guard:

```ts
import { Injectable } from '@nestjs/common';

@Injectable()
export class AuthV1Guard implements CanActivate {
    constructor(private authService: AuthService) {}
    // ...
}
```

Now, NestJS knows to use DI for the guard, and `authService` is properly injected!

## 🧠 Key Takeaway

> **If you want NestJS to inject dependencies into a class, that class must be decorated with `@Injectable()`, even if it is not a service!**

- `@Injectable()` is for **any class that participates in DI** — as a provider, a consumer, or both.
- Without it, NestJS will just use `new MyClass()` and not inject anything.

## 🪄 Analogy

Think of `@Injectable()` as a sign that says:
> "NestJS, please manage this class and its dependencies for me!"

If you want NestJS to do the wiring, you need the sign — on both the thing being injected **and** the thing receiving the injection.

---

**Remember:**
- `@Injectable()` on the provider (e.g., `AuthService`) — so it can be injected.
- `@Injectable()` on the consumer (e.g., `AuthV1Guard`) — so it can receive injections.

---

_This note was inspired by a real debugging session!_ 

Related to 
- [[Nest JS]]