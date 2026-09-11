# GTM Systems Architecture Hub

Enterprise revenue teams do not lose momentum only because of bad strategy. They lose it through unclear handoffs, inconsistent data, fragile workflows, broken routing logic, unreliable attribution, and systems that reps stop trusting.

This portfolio demonstrates how I design GTM systems that make revenue operations more reliable, visible, and scalable. The projects model real operating problems across lead ingestion, enrichment, scoring, routing, CRM handoffs, deal desk approvals, exception handling, content operations, customer health signals, and AI-assisted workflow execution.

The focus is not automation for its own sake. The focus is building explainable, testable, and governable systems that help GTM teams trust the data, understand the logic, and act faster with fewer manual gaps.

---

## What This Portfolio Demonstrates

* Event-driven GTM workflow orchestration using n8n, webhooks, REST APIs, and Node.js
* Schema-validated data contracts using JSON Schema Draft 2020-12
* Deterministic routing, scoring, escalation, and approval logic
* Dead Letter Queue patterns for exception handling, failed event review, and operational recovery
* CI validation using GitHub Actions and AJV CLI
* AI-assisted workflow design where LLMs support execution without becoming an uncontrolled source of truth
* CRM and marketing operations architecture patterns for lead lifecycle governance, enrichment, attribution, and sales handoff quality
* Practical revenue systems thinking across demand capture, pipeline movement, customer health, expansion signals, and content operations

---

## Architectural Suite Breakdown

| Pipeline Repository | Core Problem Solved | Key Tech and Guardrails |
| :--- | :--- | :--- |
| **[Pipeline 1: Agentic Orchestrator](https://github.com/derickturner-hub/pipeline-1-agentic-orchestrator)** | Unstructured lead data and manual enrichment lag | LLM tool calling, external search, dynamic scoring matrix |
| **[Pipeline 2: Lead Ingestion, Guardrails and DLQ](https://github.com/derickturner-hub/pipeline-2-lead-ingestion-dlq)** | Bad data corrupting CRM and silent webhook failures | Deterministic JSON Schema validation, Dead Letter Queue, instant Slack webhooks |
| **[Pipeline 3: SLA Round-Robin Lead Routing](https://github.com/derickturner-hub/pipeline-3-sla-round-robin-routing)** | Unfair rep distribution and slow speed-to-lead | Round-robin distribution queues, 15-minute wait timers, automated escalation routing |
| **[Pipeline 4: Customer Churn and Expansion Intelligence](https://github.com/derickturner-hub/pipeline-4-churn-expansion-intelligence)** | Reactive customer success and missed expansion signals | Product usage telemetry scoring, health threshold triggers, automated CRM staging |
| **[Pipeline 5: Multi-Channel MarTech Content Engine](https://github.com/derickturner-hub/pipeline-5-martech-content-engine)** | High-friction content repurposing and staging delays | AI content parsing, brand voice guardrails, multi-channel staging quarantine |

---

## Enterprise Architecture Data Flow

```mermaid
graph TD
    subgraph Ingestion_Layer [Ingestion and Edge API Layer]
        A1[Webhook Trigger: Lead Payload] --> B1[Pipeline 2: JSON Schema Validator]
        A2[Webhook Trigger: Content Raw Data] --> B5[Pipeline 5: AI Content Parser]
    end

    subgraph Pipeline_2 [Pipeline 2: Lead Ingestion, Guardrails and DLQ]
        B1 -->|Pass: Valid Schema| C2[Priority Scoring Matrix]
        B1 -->|Fail: Invalid Schema| D2[Dead-Letter Queue / DLQ Log]
        D2 --> E2[Slack Notification Endpoint]
    end

    subgraph Pipeline_1_3 [Pipelines 1 and 3: Orchestration, SLA Routing and Escalation]
        C2 --> F1[Pipeline 1: LLM Tool Enrichment Agent]
        F1 --> G3[Pipeline 3: Round-Robin Distribution Queue]
        G3 --> H3{15-Minute SLA Wait Timer}
        H3 -->|Claimed by Rep| I3[CRM Record Update: Closed-Won Lead]
        H3 -->|Unclaimed: SLA Breach| J3[Escalation Manager Re-route]
        J3 --> E2
    end

    subgraph Pipeline_4 [Pipeline 4: Customer Churn and Expansion Intelligence]
        K4[Product Telemetry / Usage Data] --> L4[Health Threshold Scoring]
        L4 -->|Score < Threshold| M4[Churn Risk Alert Trigger]
        L4 -->|Score > Threshold| N4[Expansion Opportunity Trigger]
        M4 --> E2
        N4 --> O4[CRM Staging / Account Executive Task Creation]
    end

    subgraph Pipeline_5 [Pipeline 5: Multi-Channel MarTech Engine]
        B5 --> P5[Brand Voice and Formatting Validation]
        P5 -->|Pass| Q5[Multi-Channel Staging: LinkedIn / GBP / CMS]
        P5 -->|Fail| R5[Editorial Review Quarantine Log]
        R5 --> E2
    end
