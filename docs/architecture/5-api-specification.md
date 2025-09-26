# 5\. API Specification

```yaml
openapi: 3.0.3
info:
  title: "FAL.ai Workflow Dashboard API"
  version: "1.0.0"
  description: "API for managing AI workflows, assets, billing, and user accounts."
servers:
  - url: "/api"
    description: "Local Development Server"
components:
  securitySchemes:
    bearerAuth:
      type: http
      scheme: bearer
      bearerFormat: JWT
security:
  - bearerAuth: []
paths:
  /workflows:
    get:
      tags: [Workflows]
      summary: "List user's workflows"
      responses:
        '200':
          description: "A list of workflows."
    post:
      tags: [Workflows]
      summary: "Create a new workflow"
      requestBody:
        required: true
        content:
          application/json:
            schema: { type: object, properties: { name: { type: string } } }
      responses:
        '201':
          description: "Workflow created successfully."
  /workflows/{workflowId}:
    put:
      tags: [Workflows]
      summary: "Update a workflow"
      parameters:
        - { name: workflowId, in: path, required: true, schema: { type: string, format: uuid } }
      requestBody:
        required: true
        content:
          application/json:
            schema: { type: object, properties: { name: { type: string }, nodes: { type: array, items: { type: object } } } }
      responses:
        '200':
          description: "Workflow updated successfully."
  /workflows/{workflowId}/run:
    post:
      tags: [Workflows]
      summary: "Execute a workflow"
      parameters:
        - { name: workflowId, in: path, required: true, schema: { type: string, format: uuid } }
      responses:
        '202':
          description: "Workflow execution accepted."
        '402':
          description: "Payment Required - Insufficient credits."
  /assets:
    get:
      tags: [Assets]
      summary: "List user's assets"
      responses:
        '200':
          description: "A list of generated assets."
  /billing/create-checkout-session:
    post:
      tags: [Billing]
      summary: "Create a Stripe Checkout session"
      responses:
        '200':
          description: "Returns the Stripe Checkout session URL."
  /webhooks/stripe:
    post:
      tags: [Billing]
      summary: "Stripe webhook handler"
      security: []
      responses:
        '200':
          description: "Webhook received."
```

-----
