# 7\. External APIs

## Fal.ai API

  * **Purpose:** To execute all generative AI models and workflows.
  * **Authentication:** API Key (`FAL_KEY` environment variable).
  * **Integration Notes:** All interaction will be encapsulated within the `Fal.ai Gateway Service`.

## Stripe API

  * **Purpose:** To handle all payment processing, subscriptions, and customer management.
  * **Authentication:** API Key.
  * **Integration Notes:** All interaction will be handled by the `Billing Service`. A webhook handler is critical for syncing subscription status.

-----
