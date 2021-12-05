# Prisma Quickstart, query database and use Prisma Studio

https://www.prisma.io/docs/getting-started/quickstart

## Quickstart

The following guide will get you up and running as quickly as possible by covering the following 3 steps:

Download a TypeScript starter project containing Prisma and an SQLite database file.
Install your dependencies.
Query some data and view the results.
Note: You need Node.js (version 12.6 or higher) for this tutorial.

### 1. Download the starter project
Open your terminal and use the following command to download the starter project.

Unix (macOS, Linux)
```java
curl -L https://pris.ly/quickstart | tar -xz --strip=2 quickstart-master/typescript/starter 
```

### 2. Install the dependencies
From the same terminal move into the project and install the dependencies:

```java
cd starter 
npm install 
```

### 3. Write a query and view the results
The following query will read all the User records from the database and return all the users and their related posts.

One of the main features of Prisma Client is the ease of working with relations. You can retrieve the posts of each user by using the include option.

Add the highlighted code to the main function in the `script.ts` file.

script.ts
```java
import { PrismaClient } from '@prisma/client'

const prisma = new PrismaClient()

// A `main` function so that you can use async/await
async function main() {
  const allUsers = await prisma.user.findMany({
    include: { posts: true },
  })
  // use `console.dir` to print nested objects
  console.dir(allUsers, { depth: null })
}

main()
  .catch((e) => {
    throw e
  })
  .finally(async () => {
    await prisma.$disconnect()
  })
```

Now run the code with the following command to see the output:

```java
npm run dev 
```

Output:
```java
> dev
> ts-node ./script.ts

[
  { id: 1, email: 'sarah@prisma.io', name: 'Sarah', posts: [] },
  {
    id: 2,
    email: 'maria@prisma.io',
    name: 'Maria',
    posts: [
      {
        id: 1,
        title: 'Hello World',
        content: null,
        published: false,
        authorId: 2
      }
    ]
  }
]
```

Note that allUsers is statically typed thanks to Prisma Client's generated types. You can observe the type by hovering over the allUsers variable in your editor.

Congratulations, you just wrote your first query with the Prisma Client and returned some data! 🎉

### Understanding what just happened
The downloaded project had Prisma all setup and included an SQLite database with some blog data.

The schema.prisma file described the User and Post models that represent tables in the SQLite database.

After downloading and installing the dependencies, you wrote a query using the Prisma Client.

This query asked for all the users and their blog posts. You then printed the results of the query to the terminal.

## Prisma Studio
```java
npx prisma studio
```


### What next?
If you're interested in learning more about Prisma, the Concepts section has all the information needed to gain a deeper understanding of how Prisma works and how it can make you more productive when working with databases.

If you are looking for guidance and workflows the Guides section has a plethora of content that covers subjects such as Database guides, Testing, Deployment and Optimizations.

Alternatively, if you want to include Prisma in an existing project the Add to existing project guide explains some core concepts as it guides you through integrating Prisma into your workflow.

Or perhaps you're looking at starting a new project with Prisma? The Start from scratch section guides you through creating a project, connecting your database and querying your data from scratch.