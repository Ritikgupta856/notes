# MongoDB & Prisma — Interview Preparation Guide

## Table of Contents

1. [MongoDB Basics](#mongodb-basics)
2. [MongoDB CRUD](#mongodb-crud)
3. [MongoDB Querying](#mongodb-querying)
4. [MongoDB Indexing](#mongodb-indexing)
5. [MongoDB Aggregation](#mongodb-aggregation)
6. [MongoDB Relationships](#mongodb-relationships)
7. [MongoDB Replication & Sharding](#mongodb-replication--sharding)
8. [MongoDB Performance](#mongodb-performance)
9. [PostgreSQL Basics](#postgresql-basics)
10. [PostgreSQL Keys & Constraints](#postgresql-keys--constraints)
11. [PostgreSQL Queries](#postgresql-queries)
12. [PostgreSQL Joins](#postgresql-joins)
13. [PostgreSQL Normalization](#postgresql-normalization)
14. [PostgreSQL Indexing](#postgresql-indexing)
15. [PostgreSQL Transactions](#postgresql-transactions)
16. [PostgreSQL Advanced](#postgresql-advanced)
17. [Prisma ORM](#prisma-orm)
18. [Comparisons](#comparisons)

---

## MongoDB Basics

### What is MongoDB? Why was it created?
**Answer:** MongoDB is a NoSQL, document-oriented database that stores data in flexible JSON-like BSON documents. It was created to solve limitations of relational databases for large-scale, unstructured, or frequently changing data. It provides schema flexibility, horizontal scalability, and developer-friendly document structure.

### MongoDB vs SQL database?
**Answer:** MongoDB stores data as documents in collections, while SQL stores data in tables with rows/columns. MongoDB is schema-flexible and better for nested/hierarchical data. SQL is stronger for complex joins, strict relationships, and transactional consistency.

| Feature | MongoDB | SQL |
|---------|---------|-----|
| Data Model | Documents (BSON) | Tables (Rows/Columns) |
| Schema | Flexible/Dynamic | Fixed/Rigid |
| Relationships | Embedding/Referencing | Foreign Keys/Joins |
| Scaling | Horizontal (Sharding) | Vertical |
| Query Language | MongoDB Query API | SQL |

### What is a document in MongoDB?
**Answer:** A document is the basic unit of data in MongoDB, stored in BSON format (Binary JSON). It's similar to a JSON object with key-value pairs. Example: `{ name: "Alice", age: 25, skills: ["JS", "React"] }`

### What is a collection in MongoDB?
**Answer:** A collection is a group of MongoDB documents, similar to a table in relational databases. Collections don't enforce schema, so documents in the same collection can have different structures.

### What is BSON?
**Answer:** BSON (Binary JSON) is MongoDB's internal binary-encoded format. It supports more data types than plain JSON (Date, ObjectId, Binary, etc.) and is more efficient for encoding and traversing.

### What is the default primary key in MongoDB?
**Answer:** Every MongoDB document has a default `_id` field which acts as the primary key. If not provided, MongoDB automatically creates an ObjectId (12-byte value: timestamp + random + counter).

### Can MongoDB have schema?
**Answer:** Yes. MongoDB is schema-flexible, not schema-less. You can enforce structure through:
- Application-level validation (Mongoose)
- Schema validation rules in MongoDB 3.2+
- Prisma schema definitions

### What are advantages of MongoDB?
**Answer:** Schema flexibility, easy horizontal scaling (sharding), fast reads for document-based data, developer-friendly JSON-like documents, strong support for nested data, and good for rapid prototyping.

### What are disadvantages of MongoDB?
**Answer:** Weaker relational modeling compared to SQL, more care needed for data consistency, poor schema design can cause duplication/query inefficiency, joins ($lookup) are less efficient than SQL joins, and no multi-collection transactions as robust as SQL.

### When should you use MongoDB?
**Answer:** Use MongoDB when data is semi-structured, changes frequently, has nested/document-style relationships, horizontal scaling is important, or when rapid development and iteration are priorities.

### When should you avoid MongoDB?
**Answer:** Avoid MongoDB when the application depends heavily on complex joins, strict relational integrity, highly normalized transactional workflows, or when data consistency requirements are extremely strict.

---

## MongoDB CRUD

### How do you insert data in MongoDB?
**Answer:**
```javascript
// Insert single document
db.users.insertOne({ name: "Alice", age: 25 })

// Insert multiple documents
db.users.insertMany([
  { name: "Bob", age: 30 },
  { name: "Charlie", age: 35 }
])
```

### How do you read data in MongoDB?
**Answer:**
```javascript
// Find all documents
db.users.find()

// Find one document
db.users.findOne({ name: "Alice" })

// Find with conditions
db.users.find({ age: { $gt: 25 } })
```

### How do you update data in MongoDB?
**Answer:**
```javascript
// Update one document
db.users.updateOne({ name: "Alice" }, { $set: { age: 26 } })

// Update multiple documents
db.users.updateMany({ age: { $lt: 30 } }, { $inc: { age: 1 } })

// Replace entire document
db.users.replaceOne({ name: "Bob" }, { name: "Bob", age: 31 })
```

### How do you delete data in MongoDB?
**Answer:**
```javascript
db.users.deleteOne({ name: "Alice" })
db.users.deleteMany({ age: { $lt: 25 } })
```

### What is the difference between find() and findOne()?
**Answer:** `find()` returns a cursor for multiple matching documents. `findOne()` returns only the first matching document (or null).

### What is projection in MongoDB?
**Answer:** Projection selects specific fields from documents instead of returning the full document.
```javascript
db.users.find({}, { name: 1, age: 1, _id: 0 }) // Only name and age
```

### What is the difference between updateOne and replaceOne?
**Answer:** `updateOne()` changes specific fields using operators ($set, $inc, etc.). `replaceOne()` replaces the entire document except `_id`.

### What are update operators in MongoDB?
**Answer:**
- `$set` — Update/add specific field
- `$unset` — Remove a field
- `$inc` — Increment numeric field
- `$push` — Add to array
- `$pull` — Remove from array
- `$addToSet` — Add to array if not exists

### What does upsert mean?
**Answer:** Upsert means update if a matching document exists, otherwise insert a new one.
```javascript
db.users.updateOne({ name: "Alice" }, { $set: { age: 25 } }, { upsert: true })
```

### What is a cursor in MongoDB?
**Answer:** A cursor is the object returned by `find()` that allows iteration over query results. You can use `toArray()`, `forEach()`, or `next()` to process results.

---

## MongoDB Querying

### How do you filter documents in MongoDB?
**Answer:**
```javascript
// Simple equality
db.users.find({ name: "Alice" })

// Comparison operators
db.users.find({ age: { $gt: 25 } })      // Greater than
db.users.find({ age: { $gte: 25 } })     // Greater than or equal
db.users.find({ age: { $lt: 30 } })      // Less than
db.users.find({ age: { $lte: 30 } })     // Less than or equal
db.users.find({ age: { $ne: 25 } })      // Not equal

// Logical operators
db.users.find({ $or: [{ age: 25 }, { age: 30 }] })
db.users.find({ $and: [{ age: { $gte: 25 } }, { age: { $lte: 35 } }] })

// In/Nin
db.users.find({ name: { $in: ["Alice", "Bob"] } })
```

### How do you query nested fields in MongoDB?
**Answer:** Use dot notation.
```javascript
db.users.find({ "address.city": "Delhi" })
db.users.find({ "address.zipcode": "110001" })
```

### How do you query array fields in MongoDB?
**Answer:**
```javascript
// Match array containing value
db.users.find({ skills: "JavaScript" })

// Match all values
db.users.find({ skills: { $all: ["JavaScript", "React"] } })

// Array element matching
db.users.find({ scores: { $gte: 80 } })

// ElemMatch for multiple conditions on same element
db.users.find({ scores: { $elemMatch: { $gte: 80, $lte: 90 } } })
```

### What is sorting in MongoDB?
**Answer:** Sort results using `sort()`.
```javascript
db.users.find().sort({ age: 1 })    // Ascending
db.users.find().sort({ age: -1 })   // Descending
db.users.find().sort({ age: 1, name: -1 }) // Multiple fields
```

---

## MongoDB Indexing

### What is an index in MongoDB?
**Answer:** An index is a data structure that improves query performance by allowing MongoDB to find documents faster without scanning the whole collection. It's similar to an index in a book.

### Why are indexes important?
**Answer:** Indexes improve read performance, reduce query time, and help scale applications. Without indexes, MongoDB performs a collection scan (checks every document).

### What are the drawbacks of indexes?
**Answer:** Indexes consume extra storage and make writes slower because indexes must also be updated on insert/update/delete.

### What types of indexes exist?
**Answer:**
- **Single-field index** — Index on one field
- **Compound index** — Index on multiple fields
- **Multikey index** — Auto-created for array fields
- **Unique index** — Ensures indexed values are unique
- **Text index** — Supports text search on string content
- **TTL index** — Auto-removes documents after time period

```javascript
// Create indexes
db.users.createIndex({ email: 1 })           // Single field
db.users.createIndex({ name: 1, age: -1 })   // Compound
db.users.createIndex({ email: 1 }, { unique: true }) // Unique
db.users.createIndex({ bio: "text" })        // Text search
```

### What is explain() in MongoDB?
**Answer:** `explain()` analyzes how MongoDB executes a query, showing whether it uses indexes efficiently.
```javascript
db.users.find({ email: "alice@example.com" }).explain("executionStats")
```

---

## MongoDB Aggregation

### What is the aggregation framework?
**Answer:** MongoDB's aggregation framework processes data through multiple transformation stages to produce computed results. It's similar to SQL GROUP BY but more powerful.

### What is an aggregation pipeline?
**Answer:** An aggregation pipeline is a sequence of stages where each stage transforms documents and passes results to the next stage.

```javascript
db.orders.aggregate([
  { $match: { status: "completed" } },           // Filter
  { $group: { _id: "$customerId", total: { $sum: "$amount" } } }, // Group
  { $sort: { total: -1 } },                      // Sort
  { $limit: 10 }                                 // Limit
])
```

### Common aggregation stages?
**Answer:**
| Stage | Purpose |
|-------|---------|
| `$match` | Filter documents (like find) |
| `$group` | Group by key and aggregate |
| `$project` | Reshape/include/exclude fields |
| `$sort` | Sort results |
| `$limit` | Limit number of results |
| `$skip` | Skip N documents (pagination) |
| `$lookup` | Join with another collection |
| `$unwind` | Deconstruct array field |
| `$addFields` | Add new computed fields |

### What is $lookup in MongoDB?
**Answer:** `$lookup` performs a join-like operation between collections.
```javascript
db.orders.aggregate([
  {
    $lookup: {
      from: "users",
      localField: "userId",
      foreignField: "_id",
      as: "user"
    }
  }
])
```

---

## MongoDB Relationships

### How are relationships handled in MongoDB?
**Answer:** Two main approaches:
1. **Embedding** — Store related data inside the same document
2. **Referencing** — Store related data in separate documents linked by IDs

### Embedding vs Referencing?
**Answer:**
| Feature | Embedding | Referencing |
|---------|-----------|-------------|
| Data Access | Single query | Multiple queries |
| Data Duplication | None | Possible |
| Update Complexity | Simple | Complex |
| Document Size | Larger | Smaller |
| Best For | Data accessed together | Large/reusable entities |

### When should you embed data?
**Answer:** Embed when:
- Related data is accessed together
- Data doesn't grow unbounded
- Data belongs naturally to parent document
- One-to-few relationships

### When should you reference data?
**Answer:** Reference when:
- Related entities are large
- Data is reused in many places
- Entities need independent updates
- One-to-many or many-to-many relationships

### What is denormalization in MongoDB?
**Answer:** Denormalization means storing duplicate data intentionally to improve read performance and reduce joins/lookups. Trade-off: faster reads but more complex updates.

---

## MongoDB Replication & Sharding

### What is replication in MongoDB?
**Answer:** Replication keeps multiple copies of data on different servers for availability and fault tolerance.

### What is a replica set?
**Answer:** A replica set is a group of MongoDB servers (typically 3+) that maintain the same data. It has one primary (receives writes) and multiple secondaries (replicate from primary).

### What is failover in MongoDB?
**Answer:** Failover is the automatic process where a secondary becomes the new primary if the original primary goes down. This ensures high availability.

### What is sharding in MongoDB?
**Answer:** Sharding is MongoDB's horizontal scaling mechanism where data is distributed across multiple servers (shards). Each shard contains a subset of the data.

### What is a shard key?
**Answer:** A shard key is the field or set of fields used to distribute data across shards. A good shard key:
- Distributes data evenly
- Avoids hotspots
- Supports common query patterns

### Does MongoDB support transactions?
**Answer:** Yes, MongoDB supports multi-document ACID transactions since version 4.0. Use them when multiple related writes must all succeed or fail together. Note: transactions add overhead.

---

## MongoDB Performance

### How do you optimize MongoDB performance?
**Answer:**
1. **Schema Design** — Design around access patterns, not normalization rules
2. **Indexes** — Create indexes for frequently queried fields
3. **Projections** — Return only needed fields
4. **Limit Results** — Use `limit()` to avoid fetching unnecessary data
5. **Analyze Queries** — Use `explain()` to identify slow queries
6. **Connection Pooling** — Reuse connections

### What is document growth issue?
**Answer:** When documents keep expanding (arrays grow unbounded), it can cause:
- Document migration to new disk locations
- Increased I/O
- Performance degradation

Solution: Use references for large arrays, or design documents with growth limits.

### What is a capped collection?
**Answer:** A capped collection is a fixed-size collection that automatically overwrites oldest documents when it reaches its limit. Useful for logging, cache, or temporary data.

```javascript
db.createCollection("logs", { capped: true, size: 1048576, max: 1000 })
```

### What is a TTL index?
**Answer:** A TTL (Time-To-Live) index automatically removes documents after a specified time period.
```javascript
db.sessions.createIndex({ createdAt: 1 }, { expireAfterSeconds: 3600 }) // 1 hour
```

### What is a covered query?
**Answer:** A covered query can be answered entirely from the index without reading the full documents. This is the fastest type of query.

### What is read/write concern?
**Answer:** 
- **Read concern** — Controls consistency/isolation of reads (local, majority, linearizable)
- **Write concern** — Controls acknowledgment level for writes (0, 1, majority)

---

## PostgreSQL Basics

### What is SQL?
**Answer:** SQL (Structured Query Language) is the standard language for defining, querying, inserting, updating, and managing data in relational databases.

### What is PostgreSQL?
**Answer:** PostgreSQL is an open-source relational database management system known for reliability, standards compliance, strong ACID support, rich SQL features, and extensibility.

### PostgreSQL vs MySQL?
**Answer:** PostgreSQL is more feature-rich and standards-compliant, especially for advanced queries, extensions, and complex data modeling. MySQL is simpler for basic use cases.

### PostgreSQL vs MongoDB?
**Answer:** PostgreSQL is relational with strong joins/transactions. MongoDB is document-oriented with flexible schema. PostgreSQL for strict consistency; MongoDB for flexible document-style data.

### What is a relational database?
**Answer:** A relational database stores data in tables with rows and columns. Relationships between tables are defined using keys (primary, foreign).

### What are tables, rows, and columns?
**Answer:**
- **Table** — Structured collection of data representing one entity type
- **Row** — A single record in a table
- **Column** — An attribute/field defining the data type

### What is schema in SQL?
**Answer:** A schema is a logical structure that organizes database objects like tables, views, indexes, and functions.

---

## PostgreSQL Keys & Constraints

### What is a primary key?
**Answer:** A primary key uniquely identifies each row in a table and cannot be null. Each table can have only one primary key.

### What is a foreign key?
**Answer:** A foreign key is a column that references the primary key of another table, enforcing relationships and referential integrity.

```sql
CREATE TABLE orders (
  id SERIAL PRIMARY KEY,
  user_id INTEGER REFERENCES users(id)
);
```

### What is a unique key?
**Answer:** A unique key ensures all values in a column (or column group) are distinct. Unlike primary key, multiple unique keys can exist per table and can contain nulls.

### What is a composite key?
**Answer:** A composite key is a key made from more than one column.

### What are other constraints?
**Answer:**
- **NOT NULL** — Column cannot store null values
- **CHECK** — Enforces condition on values
- **DEFAULT** — Provides fallback value when none specified

---

## PostgreSQL Queries

### Basic SQL commands?
**Answer:**
```sql
-- SELECT with filtering and sorting
SELECT name, email FROM users WHERE age > 25 ORDER BY name ASC;

-- Aggregate functions
SELECT department, COUNT(*) as count, AVG(salary) as avg_salary
FROM employees
GROUP BY department
HAVING COUNT(*) > 5;

-- Limit and offset (pagination)
SELECT * FROM users ORDER BY id LIMIT 10 OFFSET 20;

-- Distinct values
SELECT DISTINCT city FROM users;
```

### What is the difference between WHERE and HAVING?
**Answer:**
- `WHERE` filters rows before grouping/aggregation
- `HAVING` filters groups after aggregation

```sql
-- WHERE filters before GROUP BY
SELECT department, AVG(salary)
FROM employees
WHERE status = 'active'
GROUP BY department
HAVING AVG(salary) > 50000;
```

### What are aggregate functions?
**Answer:** Functions that perform calculations across multiple rows: `COUNT()`, `SUM()`, `AVG()`, `MIN()`, `MAX()`.

---

## PostgreSQL Joins

### What is a join?
**Answer:** A join combines rows from two or more tables based on a related column.

### Types of joins?
**Answer:**
```sql
-- INNER JOIN — Only matching rows
SELECT users.name, orders.total
FROM users
INNER JOIN orders ON users.id = orders.user_id;

-- LEFT JOIN — All left + matching right
SELECT users.name, orders.total
FROM users
LEFT JOIN orders ON users.id = orders.user_id;

-- RIGHT JOIN — All right + matching left
SELECT users.name, orders.total
FROM users
RIGHT JOIN orders ON users.id = orders.user_id;

-- FULL OUTER JOIN — All from both tables
SELECT users.name, orders.total
FROM users
FULL OUTER JOIN orders ON users.id = orders.user_id;

-- CROSS JOIN — Cartesian product (every combination)
SELECT users.name, products.name
FROM users
CROSS JOIN products;

-- SELF JOIN — Table joined with itself
SELECT e.name as employee, m.name as manager
FROM employees e
INNER JOIN employees m ON e.manager_id = m.id;
```

### INNER JOIN vs LEFT JOIN?
**Answer:**
- `INNER JOIN` — Returns only rows with matches in both tables
- `LEFT JOIN` — Returns all rows from left table, plus matches from right (NULL if no match)

---

## PostgreSQL Normalization

### What is normalization?
**Answer:** Normalization is organizing data to reduce redundancy and improve consistency by splitting data into related tables.

### Normal forms?
**Answer:**
- **1NF** — Atomic values, no repeating groups
- **2NF** — In 1NF + all non-key columns depend on full primary key
- **3NF** — In 2NF + no transitive dependencies

### Why normalize data?
**Answer:** Reduces duplication, improves consistency, makes updates safer, prevents anomalies.

### When to denormalize?
**Answer:** When read performance is critical and joins are expensive. Adds redundancy but improves query speed for read-heavy workloads.

---

## PostgreSQL Indexing

### What is an index in SQL?
**Answer:** An index is a data structure that helps the database locate rows faster without scanning the whole table.

### Types of indexes?
**Answer:**
- **B-tree** — Default, good for equality and range queries
- **Hash** — Good for equality only
- **GIN** — Good for arrays, full-text search
- **GiST** — Good for geometric/text search
- **Partial** — Indexes only rows matching a condition
- **Expression** — Index on result of expression

```sql
CREATE INDEX idx_users_email ON users(email);
CREATE INDEX idx_users_active ON users(id) WHERE status = 'active';
```

### Why are indexes important?
**Answer:** Improve query speed for filtering, sorting, and joins. Without indexes, PostgreSQL performs sequential scans.

### What is EXPLAIN ANALYZE?
**Answer:** Shows the actual execution plan and timing of a query.
```sql
EXPLAIN ANALYZE SELECT * FROM users WHERE email = 'alice@example.com';
```

---

## PostgreSQL Transactions

### What is a transaction?
**Answer:** A transaction is a group of operations treated as one unit of work. All operations succeed together or fail together.

### ACID properties?
**Answer:**
| Property | Meaning |
|----------|---------|
| **Atomicity** | All operations succeed or all fail |
| **Consistency** | Transaction moves DB from valid state to valid state |
| **Isolation** | Concurrent transactions don't interfere |
| **Durability** | Committed data survives system crashes |

```sql
BEGIN;
UPDATE accounts SET balance = balance - 100 WHERE id = 1;
UPDATE accounts SET balance = balance + 100 WHERE id = 2;
COMMIT;
```

### Isolation levels?
**Answer:**
- **Read Uncommitted** — Can see uncommitted changes (dirty reads)
- **Read Committed** — Only sees committed data (default PostgreSQL)
- **Repeatable Read** — Consistent snapshot within transaction
- **Serializable** — Strictest; transactions appear serial

### What are dirty reads, non-repeatable reads, phantom reads?
**Answer:**
- **Dirty read** — Reading uncommitted data from another transaction
- **Non-repeatable read** — Same query returns different results (another transaction committed changes)
- **Phantom read** — Same query returns different number of rows (inserts/deletes by others)

### What is MVCC?
**Answer:** Multi-Version Concurrency Control. PostgreSQL uses it to allow readers and writers to work concurrently with less locking. Each transaction sees a snapshot of the data.

---

## PostgreSQL Advanced

### What is a subquery?
**Answer:** A query nested inside another query.
```sql
SELECT name FROM users WHERE id IN (SELECT user_id FROM orders WHERE total > 100);
```

### What is a CTE?
**Answer:** Common Table Expression — a temporary named result set using `WITH`.
```sql
WITH active_users AS (
  SELECT * FROM users WHERE status = 'active'
)
SELECT * FROM active_users WHERE age > 25;
```

### What are window functions?
**Answer:** Functions that perform calculations across rows related to current row without collapsing results.
```sql
SELECT name, salary,
  ROW_NUMBER() OVER (ORDER BY salary DESC) as rank,
  AVG(salary) OVER (PARTITION BY department) as dept_avg
FROM employees;
```

### What are views and materialized views?
**Answer:**
- **View** — Virtual table based on a query (no physical storage)
- **Materialized View** — Stores query result physically (refresh needed)

### What is JSON support in PostgreSQL?
**Answer:** PostgreSQL supports JSON and JSONB types. JSONB is binary-optimized, better for indexing and querying.

```sql
CREATE TABLE events (
  id SERIAL PRIMARY KEY,
  data JSONB
);
SELECT data->>'user' FROM events;
```

### What is vacuum in PostgreSQL?
**Answer:** Vacuum is maintenance process to reclaim storage and maintain performance under MVCC. Auto-vacuum runs by default.

---

## Prisma ORM

### What is Prisma?
**Answer:** Prisma is a modern ORM for Node.js/TypeScript providing type-safe database access, schema-based modeling, migrations, and a generated client.

### What is ORM?
**Answer:** Object-Relational Mapping maps database tables/relationships into objects/methods in application code.

### Why use Prisma?
**Answer:** Type safety, improved productivity, clean schema definition, easy migrations, auto-generated query builder, excellent TypeScript integration.

### Prisma vs raw SQL?
**Answer:**
| Prisma | Raw SQL |
|--------|---------|
| Type safe | Maximum control |
| Readable queries | Complex queries possible |
| Productivity | Performance optimization |
| Auto-generated | Manual everything |

### What is the Prisma schema?
**Answer:** The central file defining models, datasource, and generator settings.
```prisma
datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

generator client {
  provider = "prisma-client-js"
}

model User {
  id    Int     @id @default(autoincrement())
  name  String
  email String  @unique
  posts Post[]
}

model Post {
  id       Int    @id @default(autoincrement())
  title    String
  author   User   @relation(fields: [authorId], references: [id])
  authorId Int
}
```

### What is Prisma Client?
**Answer:** Auto-generated query builder for application code.
```typescript
const users = await prisma.user.findMany({
  where: { age: { gt: 25 } },
  include: { posts: true }
});
```

### Prisma query methods?
**Answer:**
| Method | Purpose |
|--------|---------|
| `findUnique` | Find by unique field (id, email) |
| `findFirst` | Find first matching record |
| `findMany` | Find all matching records |
| `create` | Insert one record |
| `createMany` | Insert multiple records |
| `update` | Update one record |
| `updateMany` | Update multiple records |
| `delete` | Delete one record |
| `deleteMany` | Delete multiple records |
| `upsert` | Update or create |
| `count` | Count records |
| `aggregate` | Aggregate functions |

### select vs include in Prisma?
**Answer:**
```typescript
// select — Choose specific fields
const users = await prisma.user.findMany({
  select: { name: true, email: true }
});

// include — Bring related records
const users = await prisma.user.findMany({
  include: { posts: true }
});
```

### Prisma relations?
**Answer:**
```prisma
// One-to-one
model User {
  id    Int    @id @default(autoincrement())
  profile Profile?
}

model Profile {
  id     Int  @id @default(autoincrement())
  user   User @relation(fields: [userId], references: [id])
  userId Int  @unique
}

// One-to-many
model User {
  id    Int    @id @default(autoincrement())
  posts Post[]
}

model Post {
  id       Int  @id @default(autoincrement())
  author   User @relation(fields: [authorId], references: [id])
  authorId Int
}

// Many-to-many (implicit)
model Post {
  id         Int        @id @default(autoincrement())
  categories Category[]
}

model Category {
  id    Int    @id @default(autoincrement())
  posts Post[]
}
```

### What is Prisma Migrate?
**Answer:** Migration system for creating, applying, and tracking schema changes.
```bash
npx prisma migrate dev --name init    # Create migration
npx prisma migrate deploy            # Apply migrations
npx prisma migrate reset             # Reset database
```

### What is db push vs migrate?
**Answer:**
| db push | migrate |
|---------|---------|
| Directly syncs schema | Creates versioned migration files |
| No migration history | Full migration history |
| Good for prototyping | Good for production |
| Can cause data loss | Safe, tracked changes |

### Prisma transactions?
**Answer:**
```typescript
// Batch transaction
await prisma.$transaction([
  prisma.user.create({ data: { name: "Alice" } }),
  prisma.post.create({ data: { title: "First Post" } })
]);

// Interactive transaction
await prisma.$transaction(async (tx) => {
  const user = await tx.user.create({ data: { name: "Alice" } });
  await tx.post.create({ data: { title: "Post", authorId: user.id } });
});
```

### Common Prisma mistakes?
**Answer:**
1. Over-fetching data (use `select`)
2. Ignoring database indexes
3. Treating ORM as replacement for database knowledge
4. Running too many sequential queries (batch instead)
5. Not using transactions for related operations

### How to optimize Prisma queries?
**Answer:**
1. Use `select` to fetch only needed fields
2. Avoid over-fetching relations
3. Batch operations with `createMany`/`updateMany`
4. Use transactions for related operations
5. Add proper database indexes

---

## Comparisons

### MongoDB vs PostgreSQL
| Feature | MongoDB | PostgreSQL |
|---------|---------|------------|
| Type | Document (NoSQL) | Relational (SQL) |
| Schema | Flexible | Fixed |
| Best For | Flexible/nested data | Structured/relational data |
| Scaling | Horizontal (sharding) | Vertical |
| Joins | $lookup (slower) | Native joins (fast) |
| Transactions | Multi-doc (4.0+) | Full ACID |

### SQL vs NoSQL
| SQL | NoSQL |
|-----|-------|
| Structured data | Flexible data |
| Fixed schema | Dynamic schema |
| Vertical scaling | Horizontal scaling |
| Complex joins | Denormalized/embedded |
| Strong consistency | Eventual consistency possible |

### Prisma vs Sequelize/TypeORM
| Feature | Prisma | Sequelize/TypeORM |
|---------|--------|-------------------|
| Type Safety | Excellent | Good |
| Schema | Declarative (Prisma schema) | Decorators/definitions |
| Migrations | Built-in, tracked | Manual or plugin |
| Performance | Good | Good |
| Learning Curve | Lower | Higher |
| Raw SQL | Supported | Supported

### select vs include in Prisma
- **select** — Choose which fields to return
- **include** — Also fetch related records
