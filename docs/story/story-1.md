# Epic 1 Story: Foundation & User Authentication

## Epic Goal
Establish the complete groundwork for the application with Supabase authentication (signup, login), role-based access control (admin, free, pro), protected routes, and admin IP-lock. Result: a secure, deployable app shell ready for core features.

## Scope
- Next.js 15 app baseline with TypeScript and `shadcn/ui`
- Supabase integration (auth + database)
- Profiles schema with role enum and RLS
- Registration and Login UI
- Protected routes and role-based gates
- Admin IP-lock middleware

## Out of Scope
- Workflow execution or fal.ai integration
- Asset gallery and storage
- Billing or credits

---

## User Stories and Acceptance Criteria

### Story 1.1: Project Initialization
As a developer, I want to initialize the Next.js project with TypeScript and shadcn, so that we have a clean, standardized foundation to build upon.

Acceptance Criteria:
1. Next.js project exists using latest stable version with TypeScript configured.
2. `shadcn/ui` initialized and usable in the project.
3. Project builds and runs locally with no lint errors.
4. Code committed to a new Git repository.

### Story 1.2: Supabase Integration
As a developer, I want to connect the Next.js application to our Supabase project, so that we can leverage its database and authentication services.

Acceptance Criteria:
1. Supabase client libraries installed and configured.
2. Environment variables `NEXT_PUBLIC_SUPABASE_URL` and `NEXT_PUBLIC_SUPABASE_ANON_KEY` (and any server keys if needed) loaded from `.env.local`.
3. Successful server-side test call proves connectivity.

### Story 1.3: User & Role Schema
As a developer, I want to define the database schema for users and their roles in Supabase, so that we can store and manage user data correctly.

Acceptance Criteria:
1. `profiles` table with columns: `id` (uuid, FK to auth.users), `email` (text), `role` (enum: `admin` | `free` | `pro`).
2. RLS enabled; users can only access their own profile row.
3. Default role for new users is `free`.

### Story 1.4: Registration & Login UI
As a user, I want to create an account and log in, so that I can access the application.

Acceptance Criteria:
1. `/signup` page with email/password form using `shadcn` components.
2. `/login` page with email/password form using `shadcn` components.
3. On successful signup, user is created in Supabase Auth and a `profiles` row is inserted with role `free`.
4. On successful login, user is redirected to `/dashboard`.
5. Clear error messages on failure.

### Story 1.5: Protected Routes & Role-Based Access
As a user, I want secure access to the application, so that only authorized users with the correct role can view specific pages.

Acceptance Criteria:
1. Placeholder `/dashboard` route exists and requires authentication; unauthenticated users are redirected to `/login`.
2. Placeholder `/admin` route exists and is accessible only to `admin` role users.
3. Role checks are enforced server-side (middleware or server components) and client-side UI hides disallowed actions.

### Story 1.6: Admin IP-Lock Middleware
As an admin, I want my access restricted by IP address, so that the admin panel is maximally secure.

Acceptance Criteria:
1. Middleware applies to `/admin/**` paths.
2. Incoming request IP is checked against an allowlist from environment variables (e.g., `ADMIN_IP_ALLOWLIST`).
3. Non-whitelisted IPs receive 403 Forbidden.

---

## Non-Functional Requirements
- Security: httpOnly cookies for sessions, strict CSP, Zod validation on API inputs.
- Performance: Protected pages render within typical Next.js budgets; no unnecessary client bundles.
- Scalability: Implementation supports MVP (≤50 concurrent users) and can scale.

## Dependencies
- Supabase project and credentials available.
- Vercel (or equivalent) environment for deployment.
- DNS and environment variable management.

## Technical Notes
- Use Next.js App Router with route groups `(auth)` and `(app)` per architecture docs.
- Centralize Supabase client helpers for server and client contexts.
- Add `middleware.ts` for route protection and Admin IP-lock.
- Profiles seed or trigger to insert default role on user signup.

## Definition of Done
- All acceptance criteria across Stories 1.1–1.6 pass.
- Linting passes with zero errors; type-check passes.
- Basic E2E happy-path: signup → login → dashboard access → admin blocked for non-admin → admin allowed with correct IP.
- Documentation updated: links from PRD Epic 1 to this story.

## Test Plan
- Unit tests: auth helpers, role guards, IP-allowlist parsing.
- Integration tests: signup flow creates `profiles` row; login redirects to dashboard; RLS blocks cross-user access.
- E2E tests (Playwright):
  - Sign up and log in flows.
  - Access `/dashboard` redirects when unauthenticated.
  - Access `/admin` behavior for non-admin, admin wrong IP, admin allowed IP.

## References
- PRD: `docs/prd/6-epic-details.md#epic-1-foundation-user-authentication`
- Requirements: `docs/prd/2-requirements.md`
- Architecture: `docs/architecture/10-frontend-architecture.md`, `docs/architecture/11-backend-architecture.md`, `docs/architecture/15-security-and-performance.md`, `docs/architecture/16-testing-strategy.md`, `docs/architecture/12-unified-project-structure.md`
