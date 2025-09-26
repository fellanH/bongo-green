# 2. Requirements

## Functional Requirements
* **FR1:** The system must provide a shadcn-based dashboard interface for all user interactions.
* **FR2:** Users must be able to build and execute workflows by adding and configuring model "nodes" in a **grid-based interface**.
* **FR3:** The platform must initially integrate with the fal.ai API to run generative models, specifically supporting FLUX DEV (text-to-image) and WALT 2.2 (image-to-video).
* **FR4:** The system must support the use of custom LoRAs with compatible models.
* **FR5:** All assets generated via workflows must be displayed in a centralized gallery.
* **FR6:** Users must be able to select a generated asset from the gallery to use as an input for another workflow.
* **FR7:** The system must use Supabase for all primary data and asset management, including user data and asset metadata.
* **FR8:** The platform must offer both persistent storage (managed by Supabase) and temporary, non-persistent storage (leveraging fal.ai's hosted URLs).
* **FR9:** The application must support three distinct user roles with different permissions: Admin, Free User, and Pro User.
* **FR10:** The system must integrate with a payment provider (Stripe or Polar.sh) to handle usage-based billing for Pro users.

## Non-Functional Requirements
* **NFR1:** **Security:** The application must enforce the highest level of security due to the handling of sensitive user data and expensive, billable API calls.
* **NFR2:** **Security:** Access to the Admin role must be strictly controlled and locked down by IP address.
* **NFR3:** **Performance:** The frontend user interface must feel snappy and responsive at all times.
* **NFR4:** **Performance:** For long-running server-side processes or API calls, the UI must use skeleton loaders and provide clear feedback to the user.
* **NFR5:** **Scalability:** The architecture must support an initial MVP load of up to 50 concurrent users and be designed to scale to several thousand users without a major re-architecture.
* **NFR6:** **Usability:** The **grid-based interface** for building workflows must be intuitive and allow users to easily add, configure, and connect model nodes.
