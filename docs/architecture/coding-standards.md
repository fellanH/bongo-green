# Coding Standards

This document establishes the coding standards and development conventions for the project. All scattered standards information should reference this document as the single source of truth.

## Critical Fullstack Rules

* **Architectural Boundaries:** Code inside a `src/features/*` directory must not import from another feature directory.
* **Data Access:** All database interactions must go through the Prisma-based Repository Pattern.
* **Automated Enforcement:** We will use ESLint, Prettier, and Husky (Git hooks) to automatically enforce all standards.

## Language Standards

* **TypeScript:** Latest version across frontend and backend for type safety and code quality
* **Consistent Stack:** Same language (TypeScript) used throughout to simplify development

## Framework Conventions

* **Frontend Framework:** Next.js with App Router
* **Component Library:** shadcn/ui as the complete foundation
* **State Management:** Zustand in feature-based stores (`src/lib/stores/`)
* **CSS Framework:** Tailwind CSS (required by shadcn/ui)

## Project Structure Standards

> **📋 Complete Structure:** See [Unified Project Structure](./12-unified-project-structure.md) for detailed directory layout.

* **Feature Isolation:** Each feature in `src/features/` should be self-contained
* **Component Organization:** UI components in `src/components/ui/`, shared components in `src/components/shared/`
* **Route Groups:** Use `(app)` for protected routes, `(auth)` for public routes

## Development Workflow Standards

> **📋 Complete Workflow:** See [Development Workflow](./13-development-workflow.md) for detailed setup and processes.

* **Package Manager:** Use `pnpm` for all package management
* **Branching:** Gitflow-like model with `main`, `dev`, and `feature/*` branches
* **Database:** Use `pnpm prisma generate` and `pnpm prisma db push` for schema changes

## Testing Standards

* **Testing Framework:** Vitest and React Testing Library for unit/integration tests
* **E2E Testing:** Playwright for end-to-end testing
* **Test Organization:** Tests co-located with source code

## Performance Standards

* **React Optimization:** Use React.memo for complex components
* **CSS Approach:** Minimize custom CSS in favor of Tailwind utilities
* **Structured Logging:** Use Pino for high-performance JSON logging

-----
