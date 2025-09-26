# 12\. Unified Project Structure

> **📋 Complete Source Tree:** For detailed directory structure, organization rules, and file patterns, see the [Source Tree](./source-tree.md) document.
> **📋 Coding Standards:** For feature isolation rules and architectural boundaries, see the [Coding Standards](./coding-standards.md) document.

**Note:** This document provides a high-level overview. For complete details, see the Source Tree documentation above.

## High-Level Structure

```plaintext
/
├── prisma/              # Database schema and migrations
├── public/              # Static assets
├── src/                 # Main source code
│   ├── app/            # Next.js App Router (pages & API)
│   │   ├── (app)/      # Protected routes
│   │   ├── (auth)/     # Public authentication routes
│   │   └── api/        # Backend API routes
│   ├── components/     # React components
│   │   ├── ui/        # shadcn/ui components
│   │   └── shared/    # Reusable components
│   ├── features/      # Feature-based organization
│   └── lib/           # Shared utilities and stores
├── .env.local          # Environment variables
├── middleware.ts       # Route protection
├── next.config.mjs    # Next.js configuration
└── package.json       # Dependencies
```

## Key Organization Principles

- **Feature Isolation:** Each feature in `features/` is self-contained
- **Route Groups:** `(app)` for protected routes, `(auth)` for public routes
- **Component Hierarchy:** `ui/` for raw components, `shared/` for reusable ones
- **State Management:** Feature-based Zustand stores in `lib/stores/`

-----
