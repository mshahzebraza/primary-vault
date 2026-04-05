---
aliases:
- 🔄 Is It Okay to Use the Same Mongoose Model in Multiple Modules?
original_path: Notes/Tech Learning/Misc/Nest JS/🔄 Is It Okay to Use the Same Mongoose Model in Multiple Modules.md
base: TechLearning
path_area: Misc
categories:
- '[[TechLearning]]'
tags:
- misc
---
***My question was*:**  
If I register the same model in multiple modules using `forFeature` , does it get duplicated?

---

# ✅ The Truth: NestJS reuses the existing connection

**Nope!**  
Even if you use `forFeature` with the same model in different modules, [[Nest JS]] uses the **same internal model instance** from Mongoose’s cache.

So it doesn’t cost extra memory or CPU.

---

# 🧠 Why It Works

Mongoose maintains a **singleton model registry** per connection. Nest just maps your module’s request to the existing model from that registry.

```ts
MongooseModule.forFeature([{ name: 'Cat', schema: CatSchema }])
```


Even in 10 different modules, it refers to the same Mongoose model behind the scenes.

---

# 🧼 TL;DR

| Question                                                        | Answer                    |
| --------------------------------------------------------------- | ------------------------- |
| Does NestJS duplicate model memory if used in multiple modules? | ❌ No                      |
| Should I register in each module where I need it?               | ✅ Yes, it's good practice |

---
Related:
- [[MongoDB]]