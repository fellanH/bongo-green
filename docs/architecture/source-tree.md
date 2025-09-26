# Source Tree

**Important** Update this document if new folders are added

This document provides the complete source code organization and directory structure for the project. All scattered structure information should reference this document as the single source of truth. 

**Note:** This is a structure recomendation and can be adjusted if needed.

## Complete Directory Structure

```plaintext
/
├── prisma/                 # Prisma database schema and migrations
├── public/                 # Static assets and public files
├── src/                   # Main source code (documented structure)
│   ├── app/              # Next.js App Router pages and routing
│   │   ├── (app)/        # Protected routes (authenticated users)
│   │   │   ├── dashboard/
│   │   │   ├── workflows/
│   │   │   ├── projects/
│   │   │   └── settings/
│   │   ├── (auth)/       # Public routes (authentication)
│   │   │   ├── login/
│   │   │   ├── register/
│   │   │   └── forgot-password/
│   │   └── api/          # Next.js API Routes (serverless backend)
│   │       ├── auth/
│   │       ├── workflows/
│   │       ├── projects/
│   │       └── users/
│   ├── components/        # React component library
│   │   ├── ui/           # Raw shadcn/ui components (no customization)
│   │   │   ├── button.tsx
│   │   │   ├── input.tsx
│   │   │   ├── dialog.tsx
│   │   │   └── ...
│   │   └── shared/       # Custom, reusable components
│   │       ├── navigation/
│   │       ├── forms/
│   │       └── layouts/
│   ├── features/         # Feature-based organization (self-contained)
│   │   ├── workflows/
│   │   │   ├── components/  # Feature-specific components
│   │   │   ├── hooks/      # Feature-specific hooks
│   │   │   ├── types/      # Feature-specific types
│   │   │   └── utils/      # Feature-specific utilities
│   │   ├── projects/
│   │   │   ├── components/
│   │   │   ├── hooks/
│   │   │   └── utils/
│   │   └── auth/
│   │       ├── components/
│   │       ├── hooks/
│   │       └── utils/
│   └── lib/              # Shared utilities and configuration
│       ├── stores/       # Zustand state management (feature-based)
│       │   ├── workflow-store.ts
│       │   ├── project-store.ts
│       │   └── user-store.ts
│       ├── utils/        # Utility functions
│       ├── types/        # Shared TypeScript types
│       ├── constants/    # Application constants
│       ├── hooks/        # Shared React hooks
│       ├── auth/         # Authentication utilities
│       ├── db/          # Database utilities and Repository Pattern
│       └── api/         # API client utilities
├── .env.local           # Environment variables
├── middleware.ts        # Next.js middleware for route protection
├── next.config.mjs      # Next.js configuration
├── tailwind.config.js   # Tailwind CSS configuration
├── tsconfig.json        # TypeScript configuration
├── package.json         # Project dependencies
└── pnpm-lock.yaml      # Package manager lock file
```

## Directory Purposes & Organization Rules

### **Root Level**

- **`prisma/`** - Database schema definitions, migrations, and Prisma configuration
- **`public/`** - Static assets served directly by Next.js (images, icons, etc.)
- **`src/`** - All source code and application logic

### **Application Structure (`src/app/`)**

> **📋 Frontend Architecture:** For routing and component patterns, see [Frontend Architecture](./10-frontend-architecture.md).

#### **Route Groups**
- **`(app)/`** - Protected routes requiring user authentication
  - Includes dashboard, workflows, projects, settings
  - Protected by middleware validation
- **`(auth)/`** - Public authentication routes
  - Includes login, register, password reset
  - Accessible without authentication

#### **API Routes (`src/app/api/`)**
> **📋 Backend Architecture:** For API organization and patterns, see [Backend Architecture](./11-backend-architecture.md).

- **Structure:** RESTful API endpoints as Next.js serverless functions
- **Authentication:** All routes validate Supabase sessions
- **Data Access:** All database operations through Prisma Repository Pattern

### **Component Organization (`src/components/`)**

#### **UI Components (`src/components/ui/`)**
- **Purpose:** Raw shadcn/ui components with no project-specific customization
- **Standards:** Follow shadcn/ui conventions exactly
- **Usage:** Foundation layer for all UI elements

#### **Shared Components (`src/components/shared/`)**
- **Purpose:** Custom, reusable components used across multiple features
- **Examples:** Navigation bars, form wrappers, layout components
- **Rule:** Must be truly shared - feature-specific components go in features/

### **Feature Organization (`src/features/`)**

> **📋 Coding Standards:** For feature isolation rules, see [Coding Standards](./coding-standards.md).

#### **Critical Architecture Rules**
- **Feature Isolation:** Code inside `src/features/*` must NOT import from other feature directories
- **Self-Contained:** Each feature should include all its specific needs
- **Shared Dependencies:** Use `src/lib/` or `src/components/shared/` for cross-feature needs

#### **Feature Structure Pattern**
```plaintext
src/features/[feature-name]/
├── components/     # Feature-specific React components
├── hooks/         # Feature-specific React hooks
├── types/         # Feature-specific TypeScript types
├── utils/         # Feature-specific utility functions
└── constants/     # Feature-specific constants
```

### **Library Organization (`src/lib/`)**

#### **State Management (`src/lib/stores/`)**
- **Library:** Zustand for lightweight state management
- **Pattern:** Feature-based stores (one per major feature)
- **Naming:** `[feature-name]-store.ts`

#### **Shared Utilities (`src/lib/`)**
- **`utils/`** - Pure utility functions used across features
- **`types/`** - Shared TypeScript interfaces and types
- **`constants/`** - Application-wide constants
- **`hooks/`** - Shared React hooks
- **`auth/`** - Authentication utilities and helpers
- **`db/`** - Database utilities and Repository Pattern implementation
- **`api/`** - API client utilities and request helpers

## File Organization Conventions

### **Naming Conventions**
- **Components:** PascalCase (e.g., `WorkflowCard.tsx`)
- **Files:** kebab-case (e.g., `workflow-utils.ts`)
- **Directories:** kebab-case (e.g., `workflow-editor/`)
- **Stores:** kebab-case with suffix (e.g., `workflow-store.ts`)

### **Import/Export Patterns**
- **Feature Isolation:** No imports between `features/` directories
- **Shared Code:** Import from `lib/` or `components/shared/`
- **UI Components:** Import shadcn/ui from `components/ui/`
- **API Access:** All database operations through Repository Pattern in `lib/db/`

### **Testing Organization**
> **📋 Testing Strategy:** For complete testing approach, see [Testing Strategy](./16-testing-strategy.md).

- **Pattern:** Tests co-located with source code
- **Naming:** `[component-name].test.tsx` or `[util-name].test.ts`
- **E2E:** Playwright tests in dedicated `tests/` or `e2e/` directory

## Development Patterns

### **State Management**
- **Global State:** Zustand stores in `src/lib/stores/`
- **Local State:** React useState and useReducer within components
- **Server State:** React Query or SWR for API data fetching

### **Data Access Pattern**
- **Rule:** All database interactions through Prisma Repository Pattern
- **Location:** Repository implementations in `src/lib/db/`
- **API Routes:** Call repository methods, never direct Prisma calls

### **Authentication Flow**
- **Middleware:** `middleware.ts` protects routes based on Supabase sessions
- **Route Groups:** `(app)` requires auth, `(auth)` is public
- **API Protection:** All API routes validate sessions server-side

## Configuration Files

- **`next.config.mjs`** - Next.js framework configuration
- **`tailwind.config.js`** - Tailwind CSS styling configuration
- **`tsconfig.json`** - TypeScript compiler configuration
- **`middleware.ts`** - Next.js middleware for route protection
- **`.env.local`** - Environment variables (local development)

---