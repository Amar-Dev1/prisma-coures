# Lesson 7: Indexing in Prisma Models ⚙️

In this lesson, you'll learn:

- ✅ What is indexing?
- ✅ Why indexing matters for performance
- ✅ How to define indexes in Prisma
- ✅ Unique vs compound indexes

> Indexes make queries faster by allowing the database to quickly locate and access data. 🔍

---

## 📘 What is Indexing?

An **index** is a data structure that helps the database find rows faster based on the values in one or more columns.
Without indexes, the database has to **scan every row** (called a full table scan) to find matching results.

> Example: If you often query users by their `email`, indexing `email` will greatly improve lookup speed.

---

## ⚡ Why Indexing Matters

- ✅ Faster search, filter, and sort operations
- ✅ Reduced load on the database engine
- ✅ Crucial for performance at scale

However:

- ❌ Too many indexes can slow down `INSERT`, `UPDATE`, and `DELETE`
- ✅ Use indexes wisely based on your most common queries

---

## 🛠️ Indexing in Prisma: The `@@index` Attribute

You can define indexes at the **model level** in Prisma using the `@@index` attribute.

### ➤ Indexing a Single Field

```prisma
model User {
  id    Int     @id @default(autoincrement())
  email String

  @@index([email])
}
```

> 🔸 Creates an index on the `email` field

---

### ➤ Compound Index (Multiple Fields)

```prisma
model Order {
  id        Int     @id @default(autoincrement())
  userId    Int
  createdAt DateTime

  @@index([userId, createdAt])
}
```

> 🔸 Improves performance for queries like: `find orders by user and sort by date`

---

## 🔐 `@unique` vs `@@index`

| Prisma Attribute | Description                                      |
| ---------------- | ------------------------------------------------ |
| `@unique`        | Creates a unique index on a single field         |
| `@@index`        | Creates a non-unique index on one or more fields |
| `@@unique`       | Creates a unique **compound index**              |

### ➤ Example with `@@unique`

```prisma
model User {
  id     Int    @id @default(autoincrement())
  email  String
  name   String

  @@unique([email, name]) // Combination must be unique
}
```

---

## 📌 Best Practices

- ✅ Index fields used in `WHERE`, `ORDER BY`, or `JOIN` conditions
- ✅ Use `@unique` for natural keys like `email`, `username`
- ❌ Don’t over-index — only index what is queried frequently

---

## 🧠 Summary

✔ Indexing improves database performance\
✔ Use `@@index` for non-unique fields and combinations\
✔ Use `@unique` or `@@unique` when data uniqueness is required\
✔ Index only what improves your app’s real-world performance