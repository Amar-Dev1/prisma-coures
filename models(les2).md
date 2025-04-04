# Lesson 2: Prisma Models, Syntax & Relationships 📦

In this lesson, we’ll learn:
- ✅ How to define models in Prisma
- ✅ Prisma schema syntax
- ✅ Types of relationships: One-to-One, One-to-Many, Many-to-Many
- ✅ How to run migrations after defining models

---

## 🔶 What is a Model in Prisma?
A **model** in Prisma represents a table in your database.
Each model maps to a table, and each field inside the model is a column.

Example:
```prisma
model User {
  id    Int     @id @default(autoincrement())
  name  String
  email String  @unique
  posts Post[]
}
```
Above, we defined a `User` model with fields. The `posts` field shows a relation to a `Post` model.

---

## 🛠 Basic Field Types in Prisma
| Type    | Description          |
|---------|----------------------|
| `Int`   | Integer              |
| `String`| Text/String          |
| `Boolean` | true/false         |
| `DateTime` | Timestamp         |
| `Float` | Decimal numbers      |
| `Json`  | JSON object          |
| `Bytes` | Binary data          |

You can also use modifiers:
- `@id`: Primary key
- `@default`: Default value
- `@unique`: Unique constraint

---

## 📚 Example: User and Post Models (One-to-Many)
```prisma
model User {
  id    Int     @id @default(autoincrement())
  name  String
  email String  @unique
  posts Post[]
}

model Post {
  id        Int     @id @default(autoincrement())
  title     String
  content   String?
  published Boolean @default(false)
  authorId  Int
  author    User    @relation(fields: [authorId], references: [id])
}
```

### 🔗 Explanation:
- `User` can have many `Post` entries → One-to-Many
- `authorId` in `Post` is a foreign key linking to `User`
- `@relation` defines how the models are connected

---

## 🔗 One-to-One Relationship Example
```prisma
model User {
  id     Int     @id @default(autoincrement())
  email  String  @unique
  profile Profile?
}

model Profile {
  id     Int    @id @default(autoincrement())
  bio    String
  userId Int    @unique
  user   User   @relation(fields: [userId], references: [id])
}
```

- Each user has **one** profile, and each profile belongs to **one** user.
- `@unique` on `userId` ensures 1-to-1 relation.

---

## 🔁 Many-to-Many Relationship Example
```prisma
model User {
  id    Int     @id @default(autoincrement())
  name  String
  roles Role[]
}

model Role {
  id    Int     @id @default(autoincrement())
  name  String
  users User[]
}
```

- Prisma will automatically create a join table behind the scenes.
- No need to define the join table manually!

---

## 📤 Running Migration After Defining Models
After updating your schema:

```sh
npx prisma migrate dev --name add-models
```


---

## 🧠 Summary
✔ You now understand how to define Prisma models  
✔ You know the basic field types and relationships  
✔ You learned One-to-One, One-to-Many, and Many-to-Many relations  
✔ You know how to run migrations after updating the schema  
