# Lesson 6: Sorting & Pagination in Prisma Client 📄

In this lesson, you'll learn:
- ✅ Sorting with `orderBy`
- ✅ Pagination with `skip`, `take`
- ✅ Cursor-based pagination for efficient large queries

> Sorting and pagination are essential for building scalable, user-friendly apps like blogs, stores, and dashboards! 🧠

---

## 🔢 Sorting with `orderBy`
Sort results based on a field in ascending or descending order.

### ➤ Sort by one field
```ts
const posts = await prisma.post.findMany({
  orderBy: {
    createdAt: 'desc', // or 'asc'
  },
})
```

### ➤ Sort by multiple fields
```ts
const posts = await prisma.post.findMany({
  orderBy: [
    { published: 'desc' },
    { title: 'asc' },
  ],
})
```
> 🔸 Sort by `published` status first, then alphabetically by title.

---

## 📦 Pagination with `skip` and `take`
Use `skip` to skip a number of records and `take` to limit the number returned.

### ➤ Basic pagination
```ts
const posts = await prisma.post.findMany({
  skip: 10, // Skip first 10
  take: 5,  // Take next 5
})
```
> 🔸 Use this combo for "page X of Y" pagination logic.

---

## 🎯 Cursor-based Pagination (for performance)
Ideal for large datasets. Requires a unique identifier (like `id` or `createdAt`).

### ➤ Example
```ts
const posts = await prisma.post.findMany({
  take: 5,
  cursor: {
    id: 20, // Start after this ID
  },
  skip: 1,
})
```
> 🔸 `skip: 1` is needed to skip the cursor itself.

Cursor-based pagination is:
- ✅ More efficient than offset-based pagination in large tables
- ✅ Prevents issues when new records are inserted while paginating

---

## 🔁 Combining Sorting + Pagination
```ts
const posts = await prisma.post.findMany({
  orderBy: {
    createdAt: 'desc',
  },
  skip: 0,
  take: 10,
})
```
> 🔸 Always pair `orderBy` with `cursor` or `skip/take` for consistent results

---

## 🧠 Summary
✔ `orderBy` for sorting records by one or more fields  
✔ `skip` and `take` for classic pagination  
✔ `cursor` for fast, reliable pagination on big datasets  

### Next Lesson: Aggregations, Grouping, and Count Queries in Prisma (Lesson 7) 📊

