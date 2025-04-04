# Lesson 5: Filtering in Prisma Client 🔍

In this lesson, we'll dive deep into:

- ✅ Basic filtering: `equals`, `not`, `in`, `notIn`, `lt`, `gt`, etc.
- ✅ Advanced filtering: `AND`, `OR`, `NOT`
- ✅ String filtering: `contains`, `startsWith`, `endsWith`
- ✅ Relationship filtering using `some`, `none`, `every`, `is`, `isNot`

> Prisma provides a **powerful filtering system** using object syntax—easy to read and strongly typed! 💪

---

## 🔹 Basic Filters

### ➤ `equals`, `not`, `in`, `notIn`, `lt`, `lte`, `gt`, `gte`

```ts
const users = await prisma.user.findMany({
  where: {
    age: {
      gte: 18,
      lte: 30,
      notIn: [25, 28]
    },
    name: {
      not: "Admin"
    }
  }
})
```

> 🔸 Find users aged between 18 and 30, excluding age 25 & 28 and name not equal to "Admin"

---

## 🔹 String Filters

### ➤ `contains`, `startsWith`, `endsWith`

```ts
const posts = await prisma.post.findMany({
  where: {
    title: {
      contains: "Prisma",
      startsWith: "Intro"
    }
  }
})
```

> 🔸 Finds posts with "Prisma" in the title that also start with "Intro"

---

## 🔹 Boolean & Null Filters

```ts
const users = await prisma.user.findMany({
  where: {
    isActive: true,
    deletedAt: null
  }
})
```

> 🔸 Find all active users that haven’t been deleted

---

## 🔹 Logical Operators: `AND`, `OR`, `NOT`

```ts
const users = await prisma.user.findMany({
  where: {
    AND: [
      { email: { contains: "@gmail.com" } },
      { isActive: true }
    ],
    OR: [
      { age: { lt: 20 } },
      { age: { gt: 50 } }
    ]
  }
})
```

> 🔸 Combines filters using logic

---

## 🔹 Relationship Filters

### ➤ `some`, `none`, `every`

```ts
const users = await prisma.user.findMany({
  where: {
    posts: {
      some: {
        title: { contains: "Prisma" }
      }
    }
  }
})
```

> 🔸 Finds users who have **at least one post** with "Prisma" in the title

```ts
const usersWithNoPosts = await prisma.user.findMany({
  where: {
    posts: {
      none: {}
    }
  }
})
```

> 🔸 Finds users who have **no posts** at all

---

### ➤ `is` / `isNot` (One-to-One or BelongsTo relationships)

```ts
const posts = await prisma.post.findMany({
  where: {
    author: {
      is: {
        email: { contains: "@gmail.com" }
      }
    }
  }
})
```

> 🔸 Finds posts where the **author's email** contains `@gmail.com`

```ts
const posts = await prisma.post.findMany({
  where: {
    author: {
      isNot: {
        name: "Admin"
      }
    }
  }
})
```

> 🔸 Finds posts where author **is not** named Admin

---

## 🧠 Summary

✔ Prisma filters use intuitive object syntax\
✔ You can filter by values, strings, nulls, and relationships\
✔ Advanced logic supported: `AND`, `OR`, `NOT`\
✔ Relationships can be filtered using `some`, `none`, `is`, and more
