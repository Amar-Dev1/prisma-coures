# Lesson 4: Prisma Client Operations 🔧

In this lesson, we’ll cover:
- ✅ What is Prisma Client?
- ✅ How to use it to perform CRUD operations
- ✅ All major methods like `create`, `findUnique`, `findMany`, `update`, `delete`, and more
- ✅ Nested operations and relations

---

## 🚀 What is Prisma Client?
Prisma Client is an **auto-generated and type-safe query builder** for Node.js & TypeScript.
After defining your models and running `prisma generate`, Prisma creates a client you can import and use in your code.

```ts
import { PrismaClient } from '@prisma/client'
const prisma = new PrismaClient()
```

---

## ✨ Create Records
```ts
const newUser = await prisma.user.create({
  data: {
    name: 'Alice',
    email: 'alice@example.com',
  },
})
```
> 🔹 `create()` inserts a new record into the database.

---

## 🔍 Read Records
### ➤ Find One (by Unique Field)
```ts
const user = await prisma.user.findUnique({
  where: { email: 'alice@example.com' },
})
```

### ➤ Find by ID
```ts
const user = await prisma.user.findUnique({
  where: { id: 1 },
})
```

### ➤ Find Many
```ts
const users = await prisma.user.findMany()
```
> 🔹 You can add `where`, `orderBy`, `take`, `skip` to filter/sort (covered in Lesson 5).

---

## 📝 Update Records
```ts
const updatedUser = await prisma.user.update({
  where: { email: 'alice@example.com' },
  data: { name: 'Alice Updated' },
})
```

---

## ❌ Delete Records
```ts
const deletedUser = await prisma.user.delete({
  where: { id: 1 },
})
```

---

## 🔁 Upsert (Update or Insert)
```ts
const user = await prisma.user.upsert({
  where: { email: 'bob@example.com' },
  update: { name: 'Bob Updated' },
  create: {
    email: 'bob@example.com',
    name: 'Bob',
  },
})
```
> 🔹 Upsert checks if a record exists, then updates or inserts.

---

## 🔄 Nested Writes (Create with Related Data)
```ts
const user = await prisma.user.create({
  data: {
    email: 'john@example.com',
    name: 'John',
    posts: {
      create: [{ title: 'First Post' }, { title: 'Second Post' }],
    },
  },
})
```
> 🔹 You can create/update related data using nested operations.

---

## 🔌 Connecting Existing Relations
```ts
const post = await prisma.post.create({
  data: {
    title: 'Connected Post',
    author: {
      connect: { id: 1 },
    },
  },
})
```
> 🔹 `connect` is used to link existing records.

---

## 🧠 Summary
✔ Prisma Client lets you talk to your database in a type-safe way  
✔ You learned all basic operations: `create`, `read`, `update`, `delete`, `upsert`  
✔ You also learned about nested writes and relations  

