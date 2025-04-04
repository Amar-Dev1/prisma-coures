# Lesson 3: Prisma Attributes & Block-Level Directives 🧱

In this lesson, we’ll explore:
- ✅ What are attributes and directives in Prisma?
- ✅ Field-level vs Block-level attributes
- ✅ Common block-level attributes like `@@id`, `@@unique`, `@@index`, and more
- ✅ Use-case examples with explanation

---

## 🔹 Attributes in Prisma
**Attributes** are metadata annotations you add to your models or fields to change how Prisma handles them.

There are **two kinds**:
- **Field-level attributes** – apply to individual fields (e.g. `@id`, `@default`)
- **Block-level attributes** – apply to the whole model (e.g. `@@id`, `@@unique`, `@@index`)

Let’s break them down.

---

## 🧩 Field-Level Attributes (Quick Recap)
| Attribute       | Description |
|----------------|-------------|
| `@id`          | Declares primary key
| `@default`     | Sets a default value
| `@unique`      | Adds unique constraint to a field
| `@updatedAt`   | Updates timestamp automatically when record is updated
| `@relation`    | Declares a relation between models

Example:
```prisma
model User {
  id        Int      @id @default(autoincrement())
  email     String   @unique
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
}
```

---

## 🧱 Block-Level Attributes
Block-level attributes are defined **inside** the model block and affect **multiple fields** or the **whole model**.

### 1️⃣ `@@id([field1, field2])` — Composite Primary Key
Use this to set a **composite primary key** (i.e., more than one field).

```prisma
model Subscription {
  userId Int
  planId Int

  @@id([userId, planId])
}
```
> 🔹 Here, both `userId` and `planId` together act as a primary key.

---

### 2️⃣ `@@unique([field1, field2])` — Composite Unique Constraint
Makes a **combination** of fields unique.

```prisma
model Vote {
  userId Int
  postId Int

  @@unique([userId, postId])
}
```
> 🔹 Ensures a user can vote only once per post.

---

### 3️⃣ `@@index([field1, field2])` — Composite Index
Improves performance when filtering or sorting on multiple fields.

```prisma
model Product {
  id     Int    @id @default(autoincrement())
  name   String
  status String

  @@index([name, status])
}
```
> 🔹 Adds a DB index on `name + status` for faster querying.

---

### 4️⃣ `@@map("table_name")` — Rename Table in Database
Maps the Prisma model to a **different name** in the database.

```prisma
model Customer {
  id Int @id @default(autoincrement())
  name String

  @@map("users")
}
```
> 🔹 The table in DB will be called `users`, but in code you'll use `Customer`.

---

### 5️⃣ `@@ignore` — Ignore a Model
Tells Prisma to **ignore** the model completely.

```prisma
model OldUser {
  id Int @id

  @@ignore
}
```
> 🔹 Useful when migrating or phasing out old tables.

---

## 🧠 Summary
✔ Field-level attributes affect individual fields  
✔ Block-level attributes affect the whole model or multiple fields  
✔ You learned how to use `@@id`, `@@unique`, `@@index`, `@@map`, and `@@ignore`  
