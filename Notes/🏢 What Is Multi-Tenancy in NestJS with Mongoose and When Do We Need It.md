---
aliases:
- 🏢 What Is Multi-Tenancy in NestJS with Mongoose and When Do We Need It?
original_path: Notes/Tech Learning/Misc/Nest JS/🏢 What Is Multi-Tenancy in NestJS with Mongoose and When Do We Need It.md
base: TechLearning
path_area: Misc
categories:
- '[[TechLearning]]'
tags:
- misc
---
**What I wanted to know:**  
When do we need multiple DBs, and how does it even work in [[Nest JS]]?

---

# 🧠 What is Multi-Tenancy?

**Multi-tenancy** = One application serving **multiple distinct customers (tenants)**, while keeping their data **separated**.

## 📚 Two Multi-Tenant Approaches
There are two main patterns:
1. **Database-per-tenant** → Each tenant gets their **own MongoDB database**. More secure, more scalable, requires more infra management
2. **Collection per tenant** → One DB, but tenant data is separated logically by `tenantId`. Simpler, but data is mixed.

We'll focus on the **first** one since that’s where the NestJS + Mongoose edge case really shows up.

---

# 🧠 Use-Cases for Multi-Tenancy

|App Type|Why You Might Use Multi-Tenancy|
|---|---|
|SaaS CRM Platform|Each company (tenant) has their own users, deals, activities|
|E-learning App|Each school has isolated students, courses, exams|
|White-labeled app|Each customer runs the same app under their brand, but can’t see each other’s data|
|Health Records App|Legal requirement to isolate patient data by clinic/hospital|

---
## 🛠️ Technical Problem

If you're doing:
```ts
MongooseModule.forFeature([{ name: 'User', schema: UserSchema }])
```

…you’re registering a model tied to the **default MongoDB connection**.

But in a multi-tenant setup, you need to:
1. Dynamically choose a **different MongoDB connection per tenant**
2. Still use `Model<T>` injection and Mongoose features
    
That’s where `MongooseModule.forFeature([...], connectionName)` becomes critical.

---


# 📦 How You use the DB for multiple tenants

## Step 1: Set up multiple connections

To register a connection at boot time:

```ts
// mongoose.config.ts
export const createMongooseConnections = () => ([
  MongooseModule.forRoot('mongodb://localhost/tenantA', {
    connectionName: 'tenantA',
  }),
  MongooseModule.forRoot('mongodb://localhost/tenantB', {
    connectionName: 'tenantB',
  }),
]);
```

## Step 2: Register the model per connection

```ts
@Module({
  imports: [
    MongooseModule.forFeature(
      [{ name: 'User', schema: UserSchema }],
      'tenantA',
    ),
  ],
  providers: [UserService],
})
export class TenantAModule {}
```
…and likewise for `tenantB`.
## Step 3: Inject the model with the correct connection

```ts
@Injectable()
export class UserService {
  constructor(
    @InjectModel('User', 'tenantA') private userModel: Model<User>
  ) {}

  async findAll() {
    return this.userModel.find().exec();
  }
}
```

---

# ⚡ Advanced: Dynamic Runtime Tenant Resolution

Hardcoding connections for each tenant doesn't scale when you have 1000+ tenants.
So, you'd do this:
- Have a middleware or interceptor extract `tenantId` from the request
- Use a **custom service** to dynamically create and cache a new Mongoose connection if one doesn’t exist
- Use `Connection.model()` directly from Mongoose (not via `@InjectModel`) to get the model instance dynamically.

At large scale we might even need to setup a **Tenant Connection Caching Service** to scale up a mongoDB in a multi-tenant application.

---

# TL;DR 🥡

| Question                          | Answer                                                                                        |
| --------------------------------- | --------------------------------------------------------------------------------------------- |
| ❓ When does multi-tenancy matter? | When you serve multiple orgs/customers with isolated data                                     |
| 🧱 How is it handled in NestJS?   | By using **multiple named MongoDB connections** and `@InjectModel(modelName, connectionName)` |
| 🤯 What if tenants are dynamic?   | Build a runtime tenant resolution system with a dynamic Mongoose connection pool              |
