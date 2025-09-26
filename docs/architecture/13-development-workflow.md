# Development Workflow

## Project Initialization Checklist

1. Create branch from `dev`.
2. Run the bootstrap commands from `docs/architecture/source-tree.md`.
3. Update `docs/architecture/source-tree.md` if structure or defaults change.
4. Verify lint and build pass: `pnpm lint && pnpm build` (from `web/`).
5. Commit with a conventional message.
6. Optional: set `origin` and push the branch.

## Git Conventions

- Branching: base work from `dev`; feature branches use `feat/*`, fixes `fix/*`.
- Commit style: Conventional Commits, e.g., `feat(web): initialize Next.js app with shadcn`.
- PR requirements: concise description, link relevant story, passing lint/build checks.

## CLI Usage Policy

- Use `pnpm` for all package management commands.
- Prefer non‑interactive CLI flags for repeatability (e.g., `--yes`, `--no-turbopack`).

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
