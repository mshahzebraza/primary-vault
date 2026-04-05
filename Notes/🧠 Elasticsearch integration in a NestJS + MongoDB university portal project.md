---
sticker: emoji//1f9e0
categories:
- '[[TechLearning]]'
tags:
- misc
---

## 📌 What is Elasticsearch?

Elasticsearch is a distributed, RESTful **search and analytics engine** based on Apache Lucene. It's designed for:
- 🔍 **Full-text search**
- ⚡ **High-speed filtering and querying**
- 📊 **Real-time analytics**
- 💡 **Autocomplete, fuzzy matching, and complex queries**

---

## 🎯 Why Use Elasticsearch in Your Portal?

Your university portal serves listings for **programs, universities, and scholarships**. Elasticsearch can power:

### 🔍 **Search**
- Full-text search on program titles, descriptions, university names, etc.
- Fuzzy matching (handles typos)
- Synonyms support (e.g., B.E. ≈ Bachelor of Engineering)

### 🔄 **Filtering & Facets**
- Filter search results by:
  - Country
  - Duration
  - Tuition Fee
  - Scholarship availability
- Aggregations for fast counts (e.g., 23 programs in Germany)

### ⚡ **Autocomplete**
- Show suggestions as users type
- Example: typing “comp” returns “Computer Science”, “Computing Systems”, etc.

### 📈 **Analytics**
- Track most-searched programs, popular scholarships, etc.

---

## 🧩 Architecture Overview

```plaintext
MongoDB → (main data store)
|
| → NestJS backend → Syncs searchable fields → Elasticsearch
                                  |
                             Search Queries
                            ← Fast & relevant results
```

- MongoDB stores full data.
- Elasticsearch holds a **search index** of important fields.
- Sync required on create, update, delete.

---

## ⚙️ Setting Up Elasticsearch in NestJS

### 1. **Install the required packages**
```bash
npm install @nestjs/elasticsearch @elastic/elasticsearch
```

### 2. **Configure the module**
```ts
// app.module.ts
import { ElasticsearchModule } from '@nestjs/elasticsearch';

@Module({
  imports: [
    ElasticsearchModule.register({
      node: 'http://localhost:9200', // Replace with your ES endpoint
    }),
  ],
})
export class AppModule {}
```

---

## 🛠️ Program Search Service

### 🔸 Index a single program
```ts
@Injectable()
export class ProgramSearchService {
  constructor(private readonly esService: ElasticsearchService) {}

  async indexProgram(program: any) {
    await this.esService.index({
      index: 'programs',
      id: program._id.toString(),
      document: {
        title: program.title,
        description: program.description,
        university: program.university,
        country: program.country,
        tags: program.tags,
        hasScholarship: program.hasScholarship,
      },
    });
  }
}
```

### 🔸 Search programs
```ts
async searchPrograms(query: string) {
  const result = await this.esService.search({
    index: 'programs',
    query: {
      multi_match: {
        query,
        fields: ['title^3', 'description', 'university', 'tags'],
      },
    },
  });

  return result.hits.hits.map((hit) => hit._source);
}
```

---

## 🔁 One-Time Sync for Existing MongoDB Data

### 🧾 Bulk Index Script

```ts
async bulkIndexPrograms(programs: any[]) {
  const operations = programs.flatMap((program) => [
    { index: { _index: 'programs', _id: program._id.toString() } },
    {
      title: program.title,
      description: program.description,
      university: program.university,
      country: program.country,
      tags: program.tags,
      hasScholarship: program.hasScholarship,
    },
  ]);

  await this.esService.bulk({ refresh: true, operations });
}
```

### 📦 Sync all existing data
```ts
async syncAllProgramsToES() {
  const programs = await this.programModel.find().lean(); // Fetch from MongoDB
  await this.programSearchService.bulkIndexPrograms(programs);
  console.log(`Indexed ${programs.length} programs to Elasticsearch`);
}
```

Run this as a script/CLI command once during setup or re-indexing.

---

## 🧠 Optional: Real-time Sync with [[MongoDB Change Streams]]

If you want **automatic syncing** (advanced):
- Use MongoDB’s [Change Streams](https://www.mongodb.com/docs/manual/changeStreams/) to listen to inserts, updates, deletes.
- Trigger indexing or removal from Elasticsearch accordingly.

---

## 📚 Related Concepts & Tools

- **[[MongoDB Aggregation]]**: Useful for filtering/grouping in MongoDB if not using ES for certain queries.
- **Kibana**: Visualization/dashboard tool for Elasticsearch.
- **NestJS Task Scheduling**: Use for scheduled re-indexing if needed (`@nestjs/schedule`).
- **Elastic Cloud**: Hosted Elasticsearch by Elastic (easy setup).
- **NEST CLI Commands**: Run indexing as CLI using Nest’s custom command structure.

---

## ✅ Summary

| Feature               | MongoDB    | Elasticsearch     |
| --------------------- | ---------- | ----------------- |
| Main Data Storage     | ✅          | ❌                 |
| Full-text Search      | ⚠️ (basic) | ✅ Fast & advanced |
| Faceted Filtering     | ⚠️ Complex | ✅ Built-in        |
| Autocomplete          | ❌          | ✅                 |
| Analytics Aggregation | ⚠️         | ✅                 |
| Relevance Boosting    | ❌          | ✅                 |

> Integrating Elasticsearch is a **high-impact upgrade** for your student-facing search experience. It's totally worth the setup effort for scalable, powerful search and filtering.

---

Let me know if you'd like a boilerplate starter repo or example CLI command for syncing programs to ES.

---
Related:
- [[Nest JS]]
- [[MongoDB]]