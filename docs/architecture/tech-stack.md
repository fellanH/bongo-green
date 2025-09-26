# 3\. Tech Stack

## Technology Stack Table (Refined)

| Category | Technology | Version | Purpose | Rationale |
| :--- | :--- | :- | :--- | :--- |
| **Frontend Language** | TypeScript | latest | Adds static typing to JS | Enforces type safety, improves code quality and maintainability. |
| **Frontend Framework**| Next.js | latest | Full-stack React framework | Provides SSR, API routes, and a seamless developer experience. |
| **UI Component Lib** | shadcn/ui | latest | Composable component library | Accelerates UI development with accessible, production-ready components. |
| **State Management** | Zustand | latest | Lightweight state management | Simple, scalable, and avoids the boilerplate of more complex solutions. |
| **Backend Language** | TypeScript | latest | Adds static typing to JS | Consistent language across the stack simplifies development. |
| **Backend Framework**| Next.js API Routes| latest | Built-in serverless functions | Co-locates backend with frontend, perfect for Vercel deployment. |
| **API Style** | REST / JSON | N/A | API communication protocol | Standard, well-understood, and the default for Next.js API routes. |
| **ORM** | **Prisma** | **latest** | **Type-safe ORM** | **Enables robust Repository Pattern and simplifies data access.** |
| **Database** | PostgreSQL | 15.1 | Relational database | Provided by Supabase; powerful, reliable, and feature-rich. |
| **File Storage** | Supabase Storage | latest | S3-compatible object storage | Natively integrates with Supabase Auth for easy access control. |
| **Authentication** | Supabase Auth | latest | User authentication service | Handles all user management, social logins, and JWTs securely. |
| **Frontend Testing** | Vitest & RTL | latest | Unit/Integration testing | Modern, fast test runner with the standard library for testing React. |
| **Backend Testing** | Vitest | latest | Unit/Integration testing | Use the same fast test runner for both frontend and backend. |
| **E2E Testing** | Playwright | latest | End-to-end testing | Modern and powerful for testing critical user flows in a real browser. |
| **IaC Tool** | N/A | N/A | Infrastructure as Code | Not required; Vercel and Supabase provide a managed platform. |
| **CI/CD** | Vercel | N/A | Continuous Deployment | Native Git integration for automatic builds and deployments. |
| **Monitoring** | Vercel Analytics | N/A | Performance & usage metrics| Simple, privacy-first analytics integrated into our host. |
| **Logging** | **Pino** | **latest** | **Structured Logging** | **High-performance library for creating searchable JSON logs.** |
| **CSS Framework** | Tailwind CSS | latest | Utility-first CSS | Required by shadcn/ui and excellent for rapid, custom styling. |

-----
