# 5. Epic List

* **Epic 1: Foundation & User Authentication**
    * **Goal:** Establish the core project and get the user system working.
    * **Key Deliverables:** A live, deployable application where users can create an account, log in, and access a basic, protected dashboard based on their role (Admin, Free, Pro).
* **Epic 2: Core Workflow Execution & Asset Management (Free Tier)**
    * **Goal:** Prove out the core value proposition: generating a single AI asset for free users.
    * **Key Deliverables:** A simple form where a logged-in free user can trigger a single, admin-designated model. The generated image or video will appear in a functional, Supabase-backed asset gallery.
* **Epic 3: MVP Workflow Builder & Chaining (Pro Tier)**
    * **Goal:** Build the primary premium feature of the MVP: a multi-step workflow editor.
    * **Key Deliverables:** A list-based UI where a Pro user can add multiple model "nodes" (forms), configure them, and use the output of one node as the input for another, then execute the entire chain.
* **Epic 4: Billing Integration & Pro User Plan**
    * **Goal:** Turn the project into a monetizable product.
    * **Key Deliverables:** A fully integrated Stripe billing system. Users can view pricing, upgrade to a "Pro" plan, and their API usage will be tracked against their purchased credits.
