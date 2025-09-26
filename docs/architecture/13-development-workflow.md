# Development Workflow

## Project Initialization Checklist

1. Ensure remote `dev` exists; create if missing (see Base Branch section).
2. Create branch from `dev`.
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

## Base Branch and Remotes

- Base branch for PRs: `dev`.
- Ensure remote and base branch exist:
```bash
git fetch --all --prune
git remote -v | grep origin || git remote add origin <repo-url>
git ls-remote --exit-code origin dev || git push origin HEAD:dev
```

## Clean Working Tree Check

PRs must be created from a clean tree:
```bash
test -z "$(git status --porcelain)" || (echo "Commit or stash changes first" && exit 1)
```

## Non-interactive PR Creation (GitHub CLI)

Prereq (documented in tech stack): GitHub CLI installed and authenticated.
```bash
gh --version
gh auth status || gh auth login --hostname github.com --web

# Create PR against dev
gh pr create --base dev --head <branch> \
  --title "<conventional title>" \
  --body "<bulleted changes>" \
  --draft=false --web=false

# Optional: reviewers and labels
gh pr edit --add-reviewer team/reviewers --add-label docs --add-label architecture
```

## Commit and Merge Hygiene

- Prefer one well-scoped conventional commit per PR.
- Use fixup/squash locally to keep history clean:
```bash
git commit --fixup=<sha>
git rebase -i --autosquash dev
```
- Merge method: Squash and merge.

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
