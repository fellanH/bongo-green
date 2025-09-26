# 11\. Backend Architecture

> **📋 Tech Stack Reference:** For complete backend technology choices and versions, see the [Tech Stack](./tech-stack.md) document.
> **📋 Source Tree:** For API route organization and directory structure, see the [Source Tree](./source-tree.md) document.

## Service Architecture

  * **Structure:** Backend logic is organized into serverless functions as Next.js API Routes within `src/app/api/`.
  * **Data Access:** A Prisma-based Repository Pattern will be used to abstract all database operations.
  * **Authentication:** API routes will validate user sessions by calling Supabase server-side helpers.

-----
