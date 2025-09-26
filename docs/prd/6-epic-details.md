# 6. Epic Details

## Epic 1: Foundation & User Authentication
**Epic Goal:** This foundational epic establishes the complete technical groundwork for the application. It delivers a fully functional user authentication system using Supabase, including registration, login, and role-based access. By the end of this epic, we will have a secure, deployable application shell, ready for core features to be built upon it.

---
**Story 1.1: Project Initialization**
*As a developer, I want to initialize the Next.js project with TypeScript and shadcn, so that we have a clean, standardized foundation to build upon.*
**Acceptance Criteria:**
1.  A new Next.js project is created using the latest stable version.
2.  TypeScript is configured for the project.
3.  The `shadcn/ui` CLI is used to initialize the component library.
4.  The project is committed to a new Git repository.

---
**Story 1.2: Supabase Integration**
*As a developer, I want to connect the Next.js application to our Supabase project, so that we can leverage its database and authentication services.*
**Acceptance Criteria:**
1.  Supabase client libraries are added to the project.
2.  Environment variables for the Supabase URL and anon key are configured and loaded securely.
3.  A successful test connection to the Supabase client is demonstrated (e.g., in a server-side component).

---
**Story 1.3: User & Role Schema**
*As a developer, I want to define the database schema for users and their roles in Supabase, so that we can store and manage user data correctly.*
**Acceptance Criteria:**
1.  A `profiles` table is created with columns for user ID, email, and role.
2.  A custom `enum` type for roles (`admin`, `free`, `pro`) is created and applied to the role column.
3.  Row Level Security (RLS) policies are enabled to ensure users can only access their own profile data.

---
**Story 1.4: Registration & Login UI**
*As a user, I want to be able to create a new account and log in, so that I can access the application.*
**Acceptance Criteria:**
1.  A `/signup` page is created with a form for email and password using `shadcn` components.
2.  A `/login` page is created with a form for email and password using `shadcn` components.
3.  Successful registration creates a new user in Supabase Auth and a corresponding entry in the `profiles` table with a default 'free' role.
4.  Successful login redirects the user to the dashboard.
5.  Appropriate error messages are shown for failed attempts.

---
**Story 1.5: Protected Routes & Role-Based Access**
*As a user, I want secure access to the application, so that only authorized users with the correct role can view specific pages.*
**Acceptance Criteria:**
1.  A placeholder `/dashboard` page is created.
2.  The `/dashboard` page is a protected route, redirecting unauthenticated users to `/login`.
3.  A placeholder `/admin` page is created.
4.  The `/admin` page is protected and only accessible to users with the 'admin' role.

---
**Story 1.6: Admin IP-Lock Middleware**
*As an admin, I want my access restricted by IP address, so that the admin panel is maximally secure.*
**Acceptance Criteria:**
1.  Next.js middleware is created for the `/admin/**` route path.
2.  The middleware checks the incoming request's IP against a whitelist in the environment variables.
3.  Requests from non-whitelisted IPs to any admin route are blocked with a 403 Forbidden error.

---
## Epic 2: Core Workflow Execution & Asset Management (Free Tier)
**Epic Goal:** This epic delivers the core **Free Tier experience**. We will integrate with the fal.ai API, allowing a logged-in free user to execute a single, admin-designated workflow (defaulting to FLUX DEV). The resulting asset will be saved and displayed in the user's gallery.

---
**Story 2.1: Fal.ai API Client**
*As a developer, I want to create a secure API client for the fal.ai service, so that our backend can make authenticated requests to generate content.*
**Acceptance Criteria:**
1.  A new server-side service/module for the fal.ai client is created.
2.  The fal.ai API key is securely loaded from environment variables and is never exposed to the client-side.
3.  A function exists to trigger a workflow run on fal.ai, handling authentication and request formatting.
4.  Error handling is implemented for common API failures (e.g., auth errors, invalid requests).

**Dev Notes:**
* **Client Installation:** The `@fal-ai/client` package is required.
* **Authentication:** The client uses an API Key for authentication. This must be set as a `FAL_KEY` environment variable.
* **Call Types:** The client can call pre-defined **Workflows** (e.g., `"workflows/username/workflow-name"`) or **Hosted Models** directly (e.g., `"fal-ai/flux/dev"`).
* **Submission Options:**
    * **Normal Return (`fal.subscribe`):** Waits for the job to complete. Good for immediate needs and provides progress updates via `onQueueUpdate`.
    * **Streaming (`fal.stream`):** For real-time results from supported models.
    * **Queuing (`fal.queue.submit`):** For long-running jobs. It returns a `request_id` to check status and fetch results later. Supports a `webhookUrl` for notifications.
* **File Handling:** Inputs can be URLs. The client provides `fal.storage.upload` to upload local files and get a URL. It will also auto-upload binary objects passed directly as input.

---
**Story 2.2: Asset Database Schema**
*As a developer, I want to create a database schema for storing asset metadata, so that we can manage and display generated content.*
**Acceptance Criteria:**
1.  A new `assets` table is created in Supabase.
2.  The table includes columns for asset ID, owner ID (foreign key to `profiles`), the public URL from fal.ai, and the workflow input parameters (as JSONB).
3.  Row Level Security policies are added to ensure users can only view and manage their own assets.

---
**Story 2.3: Simple Workflow Execution Page**
*As a free user, I want a simple form to generate an image using the basic model, so that I can test the core functionality of the platform.*
**Acceptance Criteria:**
1.  A new protected page `/generate` is created.
2.  The page contains a simple `shadcn` form with a text input for a prompt.
3.  Submitting the form triggers a server-side API route in our Next.js backend.
4.  The API route executes the **system-wide basic model** (initially hardcoded to `"fal-ai/flux/dev"`) with the user's prompt.
5.  While the job is running, the UI displays a loading state.

---
**Story 2.4: Save and Display Generated Asset**
*As a free user, I want to see the image I generated and have it saved to my account, so that I can access it later.*
**Acceptance Criteria:**
1.  Upon successful completion of the fal.ai job, the backend API route receives the output URL.
2.  A new record is created in the `assets` table with the asset URL, owner ID, and prompt details.
3.  The API route responds to the frontend with the newly created asset record.
4.  The frontend redirects the user to the Asset Gallery page, displaying the newly generated image.

---
**Story 2.5: Asset Gallery UI**
*As a free user, I want to view all the assets I have previously generated, so that I can manage my creations.*
**Acceptance Criteria:**
1.  A new protected page `/gallery` is created.
2.  The page fetches and displays all assets owned by the currently logged-in user from the `assets` table.
3.  Assets are displayed in a responsive grid layout using `shadcn` card components.
4.  Each asset card displays the generated image and the prompt used to create it.

---
**Story 2.6: Admin Model Selection**
*As an admin, I want to designate one model as the default for free users, so I can control the free tier offering.*
**Acceptance Criteria:**
1.  An admin-only page (`/admin/settings`) is created for platform settings.
2.  The page has a form to select a model ID to be used by all free tier users.
3.  For the MVP, this setting is hardcoded in the backend to `"fal-ai/flux/dev"`, and the UI is not required. The story serves as a placeholder for the backend logic.

---
## Epic 3: MVP Workflow Builder & Chaining (Pro Tier)
**Epic Goal:** This epic delivers the core **Pro Tier feature**. We will build the list-based UI that allows Pro users to dynamically add, configure, and chain multiple model nodes, transforming the application into a true workflow-building tool.

---
**Story 3.1: Workflow Data Schema**
*As a developer, I want to create a database schema for workflows and their nodes, so that users can save and manage their creations.*
**Acceptance Criteria:**
1.  A new `workflows` table is created in Supabase with columns for workflow ID, name, and owner ID.
2.  A new `nodes` table is created with columns for node ID, workflow ID, model ID (e.g., `"fal-ai/flux/dev"`), and input configuration (JSONB).
3.  A `position` column is added to the `nodes` table to maintain their order.
4.  RLS policies are added so users can only manage their own workflows.

---
**Story 3.2: Workflow Editor UI Shell**
*As a **pro user**, I want a dedicated page to build a workflow, so I can start creating.*
**Acceptance Criteria:**
1.  A new dynamic, protected route `/workflows/[id]` is created.
2.  **The `/workflows/**` pages are only accessible to users with the 'pro' or 'admin' role. Free users are shown an upgrade prompt.**
3.  The page displays the workflow's name, a "Run Workflow" button, and an "Add Node" button.
4.  The page has a list area that is initially empty, ready to display nodes.

---
**Story 3.3: Add and Configure a Node**
*As a pro user, I want to add a model to my workflow and configure its inputs, so I can define a step in my process.*
**Acceptance Criteria:**
1.  Clicking "Add Node" lets the user select from a hardcoded list of available models.
2.  Selecting a model adds a new `shadcn` form to the node list in the UI.
3.  The form contains fields for all the model's inputs (e.g., a "prompt" text area).
4.  Saving the form updates the workflow's state on the frontend.

---
**Story 3.4: Save Workflow State**
*As a pro user, I want my workflow to be saved automatically, so I don't lose my work.*
**Acceptance Criteria:**
1.  Adding, editing, or removing a node triggers an API call to the backend.
2.  The backend API saves the entire workflow and its nodes to the Supabase tables.
3.  When a user visits a workflow page, the saved nodes are fetched and displayed correctly.

---
**Story 3.5: Implement Workflow Chaining Logic**
*As a pro user, I want to use the output of one node as the input for another, so I can create a multi-step process.*
**Acceptance Criteria:**
1.  A node's input form includes an option to use the output from a previous node (e.g., a dropdown showing "Output from Node 1").
2.  The backend execution logic is updated to run nodes sequentially, waiting for the first node to complete before starting the second.
3.  The output URL from the first node is correctly passed as an input parameter to the second node.

---
**Story 3.6: Execute and Monitor a Chained Workflow**
*As a pro user, I want to run my entire chained workflow and see the final result, so I can get the benefit of my creation.*
**Acceptance Criteria:**
1.  The "Run Workflow" button triggers the backend to execute all nodes in sequence.
2.  The UI displays the overall status of the workflow (e.g., "Running Node 1 of 2," "Complete").
3.  The final asset(s) from the last node are saved to the user's asset gallery.
4.  The user is redirected to the gallery to see the final output upon completion.

---
## Epic 4: Billing Integration & Pro User Plan
**Epic Goal:** This final epic turns our functional application into a commercially viable product. We will integrate Stripe to handle payments and subscriptions, creating a seamless upgrade path for users who want to access the Pro features. The stories will cover everything from the user-facing pricing page to the backend logic for tracking and managing API credit usage.

---
**Story 4.1: Stripe Integration & Product Setup**
*As a developer, I want to integrate the Stripe SDK and configure our product plans, so that we have a foundation for billing.*
**Acceptance Criteria:**
1.  The Stripe Node.js SDK is added to the backend.
2.  Stripe API keys are securely managed via environment variables.
3.  A "Pro Plan" product with usage-based pricing for "credits" is created in the Stripe dashboard.
4.  A webhook endpoint is created in our backend to listen for Stripe events, and it is registered with Stripe.

---
**Story 4.2: Pricing & Upgrade Page UI**
*As a free user, I want to see the available plans and their features, so I can decide to upgrade.*
**Acceptance Criteria:**
1.  A new `/pricing` page is created.
2.  The page displays "Free" and "Pro" tiers, clearly listing the features of each (e.g., "Multi-step Workflows" for Pro).
3.  The Pro plan shows the price for a monthly subscription and the cost per credit.
4.  An "Upgrade to Pro" button is prominent.

---
**Story 4.3: Implement Stripe Checkout Flow**
*As a free user, I want a simple and secure way to subscribe to the Pro plan, so I can unlock premium features.*
**Acceptance Criteria:**
1.  Clicking "Upgrade to Pro" on the pricing page redirects the user to a Stripe-hosted Checkout session.
2.  Upon successful payment, the Stripe webhook receives a `checkout.session.completed` event.
3.  The webhook handler updates the user's role in our Supabase `profiles` table from 'free' to 'pro'.
4.  The user is redirected to a success page and now has access to Pro features.

---
**Story 4.4: Credit Usage Tracking**
*As a developer, I want to track a Pro user's API credit consumption, so that we can bill them accurately.*
**Acceptance Criteria:**
1.  A `credits` column is added to the `profiles` table to store a user's balance.
2.  When a Pro user runs a workflow, the backend calculates the "credit cost" (for MVP, a fixed cost per node run).
3.  The user's credit balance is decremented after a successful job.
4.  Workflows are blocked if the user's credit balance is insufficient to cover the cost.

---
**Story 4.5: Billing & Usage Dashboard**
*As a pro user, I want to see my current credit balance and manage my subscription, so I can stay in control of my spending.*
**Acceptance Criteria:**
1.  A new `/billing` page is created, accessible only to Pro users.
2.  The page displays the user's current credit balance.
3.  The page includes a button that securely redirects the user to the Stripe Customer Portal for managing payment methods and viewing invoices.

