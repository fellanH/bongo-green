# 10\. Frontend Architecture

> **📋 Tech Stack Reference:** For complete frontend technology choices and versions, see the [Tech Stack](./tech-stack.md) document.
> **📋 Coding Standards:** For architectural boundaries and development standards, see the [Coding Standards](./coding-standards.md) document.
> **📋 Source Tree:** For complete directory structure and organization patterns, see the [Source Tree](./source-tree.md) document.

## Component Organization

> **Note:** This is a high-level overview. See Source Tree documentation for complete structure details.

```plaintext
src/
├── app/              # Next.js App Router
├── components/
│   ├── ui/          # Raw shadcn/ui components
│   └── shared/      # Custom, reusable components
└── features/
    └── workflows/
        └── components/ # Components specific to a feature
```

## State Management

  * **Structure:** State will be managed in feature-based stores (`src/lib/stores/`).
  * **Library:** Zustand.

## Routing

  * **Structure:** Routing is managed by the Next.js App Router's directory structure, using Route Groups like `(app)` for protected routes and `(auth)` for public routes.
  * **Protection:** Middleware (`src/middleware.ts`) will be used to protect routes based on Supabase session.

-----
