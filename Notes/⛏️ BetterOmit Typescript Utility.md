---
original_path: Notes/Tech Learning/Misc/⛏️ BetterOmit Typescript Utility.md
base: TechLearning
path_area: Misc
categories:
  - "[[TechLearning]]"
  - "[[Misc]]"
---
The built-in `Omit<T, K>` is great but sometimes:
- You want to omit **multiple nested keys**
- You want to **omit deeply**, not just at the top level
- You want a **type-safe, infer-friendly** utility for complex shapes


## BetterOmit

```ts title:"BetterOmit"
// BetterOmit for top-level
type BetterOmit<T, K extends keyof T> = Pick<T, Exclude<keyof T, K>>;
```
This is the same as built-in `Omit<T, K>`. Just included for comparison.

## DeepOmit

```ts title:'DeepOmit'
// DeepOmit for nested key
type Primitive = string | number | boolean | bigint | symbol | null | undefined;

type DeepOmit<T, K> = {
  [P in keyof T as P extends keyof K ? never : P]: T[P] extends Primitive
    ? T[P]
    : T[P] extends Array<infer U>
      ? DeepOmit<U, K[P]>[]
      : T[P] extends object
        ? DeepOmit<T[P], K[P]>
        : T[P];
} & {
  [P in keyof K & keyof T]?: T[P] extends object
    ? T[P] extends Array<infer U>
      ? DeepOmit<U, K[P]>[]
      : DeepOmit<T[P], K[P]>
    : never;
};

```


## Usage Examples

```ts
// DeepOmit
type User = {
  id: string;
  email: string;
  profile: {
    name: string;
    avatar: string;
    sensitiveNote: string;
  };
};

type SafeUser = DeepOmit<User, { profile: 'sensitiveNote' }>;
// Result type will omit profile.sensitiveNote


type BetterUser = BetterOmit<User, 'profile' | 'id'>
// Result type will only contain id in the object
```

## TL;DR 🥡

| Utility Name | Use Case                          |
| :----------- | :-------------------------------- |
| `MyOmit`     | Basic omission (same as built-in) |
| `DeepOmit`   | Omit nested/deep properties       |
