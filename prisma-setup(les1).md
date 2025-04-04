# Lesson 1: Introduction to Prisma & Setup 🚀

## What is Prisma? 🤔
Prisma is a next-generation ORM (Object-Relational Mapping) tool for Node.js and TypeScript. It helps developers interact with databases in an intuitive and type-safe way. Instead of writing raw SQL queries, you can use Prisma's elegant API to manage your data.

### Why Use Prisma? 🏆
- **Type Safety**: You get autocompletion and type safety while writing database queries.
- **Migrations Made Easy**: Prisma handles database schema changes with built-in migration tools.
- **Database Agnostic**: Supports PostgreSQL, MySQL, SQLite, SQL Server, and MongoDB.
- **Great for Full-Stack Development**: Works well with frameworks like Next.js, Express, and Fastify.

---

## Step 1: Setting Up a Node.js Project 🛠️
Before using Prisma, we need a Node.js project.

1. **Install Node.js** (if you haven't already): Download and install from [nodejs.org](https://nodejs.org/).
2. **Check if Node.js is installed**:
   ```sh
   node -v  # Should print the Node.js version
   npm -v   # Should print the npm version
   ```
3. **Create a new project**:
   ```sh
   mkdir prisma-tutorial
   cd prisma-tutorial
   npm init -y
   ```
   This initializes a `package.json` file, which keeps track of dependencies.

---

## Step 2: Installing Prisma 📦
Now, let's install Prisma and its dependencies.

```sh
npm install prisma --save-dev
npm install @prisma/client
```

- `prisma` is the CLI tool for managing Prisma.
- `@prisma/client` is the library that allows us to interact with the database.

---

## Step 3: Initializing Prisma 🎉
Run the following command to set up Prisma in your project:

```sh
npx prisma init
```

This creates a `prisma` folder and a `.env` file. Inside the `prisma` folder, you'll find `schema.prisma`, which is the main Prisma configuration file.

---

## Step 4: Configuring a Database 🗄️
Prisma needs a database to work with. By default, it sets up SQLite. Let's modify `prisma/schema.prisma` to use SQLite:

```prisma
// prisma/schema.prisma

generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "sqlite"
  url      = env("DATABASE_URL")
}
```

Now, open the `.env` file and update the database connection URL:

```env
DATABASE_URL="file:./dev.db"
```

---

## Step 5: Creating the First Migration 🚀
Now, let’s apply the database schema:

```sh
npx prisma migrate dev --name init
```

This will:
- Create the database file (`dev.db` for SQLite).
- Generate Prisma migration files.

---

## Step 6: Generating Prisma Client 🛠️
To use Prisma in your code, generate the Prisma client:

```sh
npx prisma generate
```

This step ensures that Prisma can interact with your database.

---

## Summary 📌
✔ We installed Node.js and initialized a new project.  
✔ We installed Prisma and set up a database.  
✔ We configured Prisma with SQLite.  
✔ We ran a migration and generated Prisma Client.  

