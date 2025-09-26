# 13\. Development Workflow

> **📋 Coding Standards:** For automated enforcement with ESLint, Prettier, and Husky, see the [Coding Standards](./coding-standards.md) document.

## Local Development Setup

1.  Clone repository.
2.  Install dependencies with `pnpm install`.
3.  Set up `.env.local` file with required keys (Supabase, Stripe, etc.).
4.  Run `pnpm prisma generate` and `pnpm prisma db push`.
5.  Start the dev server with `pnpm dev`.

## Source Control & Branching Strategy

  * **Model:** A Gitflow-like model with `main`, `dev`, and `feature/*` branches.
  * **Process:** Features are developed on `feature` branches, create Pull Requests to `dev`.
  * **Deployments:** Vercel deploys `main` to Production and all other branches to Preview.

-----
