# Prisma (Stater lesson)
Prisma ORM is a next-generation Node.js and TypeScript ORM that unlocks a new level of developer experience when working with databases thanks to its intuitive data model, automated migrations, type-safety & auto-completion.

## Getting started with prisma (phase1)

<p align="center">
    <a href="#" style="display: block;" align="center">
        <img src="https://i.pinimg.com/originals/84/7c/a0/847ca0dc00a4d3038bfda6cb66e14613.gif" alt="kenpachi zaraki" width="60%" />
    </a>
</p>

The perequisites for this starter project includes:
- Node.js 18+ installed
- A Prisma Postgres database (or any PostgreSQL database)
- A Vercel account (if you want to deploy your application)

## Begin to setup the Next.JS project
for the completeness of the project we install these:
1. TypeScript
2. ESLint
3. Tailwind CSS
4. No `src` directory
5. App router
6. Turbopack
7. No customized import alias
Then navigate to your project directory

## Setting up the Prisma (ORM)

<p align="center">
    <a href="#" style="display: block;" align="center">
        <img src="https://cdnlogo.com/logos/p/25/prisma.svg" alt="kenpachi zaraki" width="60%" />
    </a>
</p>

First, we need to install a few dependencies. 
```bash
npm install prisma --save-dev
npm install tsx --save-dev
npm install @prisma/extension-accelerate
```
we'll be using a Prisma Postgrese database so we're going to use the  ` @prisma/extension-accelerate` package.

Next we run `prisma init` to initialize the prisma ORM in our project.

```bash
npx prisma init
```
In the new `prisma` directory comes with a schema.prisma file inside it, this is where we define the database models.

```typescript
generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

model User {
  id    Int     @id @default(autoincrement())
  email String  @unique
  name  String?
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
This represents a blog posts with each post having a user as an author and each user can have many post's.

### Save the Database connection string
with the Prisma Postgrs we have a `DATABASE_URL` that you store in the .`env` file.

```bash
DATABASE_URL = "Your URL"
```
save the database connection string and apply the schema to the database `using prisma migrate dev`

```bash
npx prisma migrate dev --name init
```

## Output
![alt text](image.png)

This creates an initial migration creating the User and Post tables and applies that migration to the database.

This is a [Next.js](https://nextjs.org) project bootstrapped with [`create-next-app`](https://nextjs.org/docs/app/api-reference/cli/create-next-app).

## Getting Started

First, run the development server:

```bash
npm run dev
# or
yarn dev
# or
pnpm dev
# or
bun dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

You can start editing the page by modifying `app/page.tsx`. The page auto-updates as you edit the file.

This project uses [`next/font`](https://nextjs.org/docs/app/building-your-application/optimizing/fonts) to automatically optimize and load [Geist](https://vercel.com/font), a new font family for Vercel.

## Learn More

To learn more about Next.js, take a look at the following resources:

- [Next.js Documentation](https://nextjs.org/docs) - learn about Next.js features and API.
- [Learn Next.js](https://nextjs.org/learn) - an interactive Next.js tutorial.

You can check out [the Next.js GitHub repository](https://github.com/vercel/next.js) - your feedback and contributions are welcome!

## Deploy on Vercel

The easiest way to deploy your Next.js app is to use the [Vercel Platform](https://vercel.com/new?utm_medium=default-template&filter=next.js&utm_source=create-next-app&utm_campaign=create-next-app-readme) from the creators of Next.js.

Check out our [Next.js deployment documentation](https://nextjs.org/docs/app/building-your-application/deploying) for more details.
