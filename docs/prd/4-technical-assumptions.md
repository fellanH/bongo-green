# 4. Technical Assumptions

## Repository Structure: Monorepo
We will use a standard Next.js project structure, which acts as a **monorepo** by containing both the frontend application and the backend API routes in a single repository. This is the simplest and most efficient structure for the MVP.

## Service Architecture: Monolith
For the MVP, we will build a single, monolithic backend service co-located within the Next.js application. This service will handle user authentication, workflow management, and communication with external APIs. This approach reduces complexity and allows for faster iteration.

## Testing Requirements: Unit + Integration
The testing strategy will require both unit tests for individual components and functions, as well as integration tests to verify interactions between the frontend, backend, and external services like Supabase and fal.ai.

## Additional Technical Assumptions and Requests

> **📋 Complete Tech Stack:** For detailed technology choices, versions, and rationales, see the [Tech Stack](../architecture/tech-stack.md) document.

* **Frontend Framework:** Next.js with TypeScript (React-based, works seamlessly with shadcn).
* **Backend Framework:** Node.js with TypeScript. Backend logic will be implemented as serverless API routes within the Next.js application.
* **Database & Auth:** Supabase will be used for the primary PostgreSQL database, user authentication, and persistent asset storage.
* **Primary External API:** The fal.ai API is the initial and primary integration for generative AI models.
* **Payment Provider:** Stripe will be the initial payment provider for usage-based billing.
* **Deployment Target:** Vercel is the preferred platform for deploying the Next.js application, as it offers a streamlined developer experience and seamless integration.
