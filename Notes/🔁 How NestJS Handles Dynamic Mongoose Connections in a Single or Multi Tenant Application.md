---
aliases:
  - 🔁 How NestJS Handles Dynamic Mongoose Connections in a Single/Multi-Tenant Application
original_path: Notes/Tech Learning/Misc/Nest JS/🔁 How NestJS Handles Dynamic Mongoose Connections in a Single or Multi Tenant Application.md
base: TechLearning
path_area: Misc
categories:
  - "[[TechLearning]]"
  - "[[Misc]]"
---

**My follow-up question:**
If I dynamically create connections per tenant in [[Nest JS]], do they stay open? And how do I scale with many tenants?

---

# Are multiple Mongoose connections kept alive?
## ✅ Yes — Mongoose connections are persistent

Each time you call `mongoose.createConnection()`, a new TCP connection opens and stays active unless you explicitly `.close()` it.

When you dynamically connect a new tenant like this:

```ts
mongoose.createConnection(uri);
```

Mongoose:
- Opens a **new TCP socket** to the MongoDB server
- Keeps that connection **alive** (idle but open) for reuse
- Will **not close it** unless you explicitly call `.close()` or `.disconnect()`

> So yes, if 10 tenants hit your app over time, and each triggers a new DB connection, you now have 10 open Mongoose connections.

And by the time you hit 1000 tenants...? 😬 You got it...

---

# 🔁 How do we scale with 1000+ tenants?
## 🧠 Scalable Strategy: Use a Connection Pool & Cache

Create a `TenantConnectionService` that:
- Keeps a **cache** of existing Mongoose connections by `tenantId`
- Reuses existing connections
- Dynamically creates new ones only **on first request** per tenant
- Optionally includes a **TTL cache** or **[[LRU eviction]]** strategy if you have tons of tenants

```ts
class TenantConnectionService {
  private connections = new Map<string, Connection>();

  async getConnection(tenantId: string): Promise<Connection> {
    if (this.connections.has(tenantId)) {
      return this.connections.get(tenantId);
    }

    const uri = buildUriFromTenantId(tenantId);
    const connection = await mongoose.createConnection(uri).asPromise();

    this.connections.set(tenantId, connection);
    return connection;
  }
}
```

### 🧼 Tips
- Close stale connections if needed
- Use `mongoose.createConnection()` (non-global)
- Use `connection.model()` instead of `@InjectModel` for dynamic tenant setups

This is how **SaaS giants** handle it at scale.

---

# ❓ What about Single-Tenant?

## ⚙️ When is the MongoDB connection established?
It connects **on app boot** (if using `forRoot()`), and keeps a pool alive.

```ts
MongooseModule.forRoot('mongodb://localhost/singleTenantDb')
```

Then Nest + Mongoose:
- Opens connection on application startup
- Keeps it alive
- Uses a **connection pool** under the hood (default ~5 sockets)
- Auto-reconnects on failures (depending on options)

Use `.forRootAsync()` to delay or make the connection async if needed.

---

# 💡 TL;DR

| Question | Answer |
|---|---|
| Will connections stay active after creation? | ✅ Yes, until manually closed |
| How does this scale to 1000+ tenants? | 🔁 Connection cache — reuse if exists, create on-demand |
| In a single-tenant app, when does connection happen? | 🕐 At **app boot time**, not on first request |
| Can I manage memory/connection count? | ✅ Add TTL/LRU caching & close stale connections |

---

## Related Notes
- [[Nest JS]]
- [[MongoDB]]
