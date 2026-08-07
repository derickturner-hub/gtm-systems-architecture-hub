# Enterprise RevOps Architecture Portfolio

Master architecture repository for production-ready Revenue Operations automation pipelines. This organization contains event-driven systems built around strict JSON Schema contracts, deterministic JavaScript scoring modules, and n8n workflow orchestration.

---

## System Architecture

```mermaid
flowchart TD
    subgraph Pipeline 1: Content Production Engine
        A1[Campaign Brief Payload] --> B1[Draft 2020-12 Schema Validation]
        B1 --> C1[Multi-Agent Content Execution]
        C1 --> D1[n8n Campaign Publishing Workflow]
    end

    subgraph Pipeline 2: Lead Enrichment & Scoring
        A2[Inbound Lead Event] --> B2[Draft 2020-12 Schema Validation]
        B2 --> C2[Parallel Firmographic & Technographic Enrichment]
        C2 --> D2[0-100 Deterministic Matrix Scoring]
        D2 --> E2[Tier 1 MQL / Tier 2 SQL / Tier 3 Nurture / DLQ]
    end

    subgraph Pipeline 3: Churn & Expansion Intelligence
        A3[Account Telemetry Event] --> B3[Draft 2020-12 Schema Validation]
        B3 --> C3[Contract Metadata Aggregator]
        C3 --> D3[0-100 Account Health Matrix Engine]
        D3 --> E3[Slack Risk Alert / Expansion Opportunity / CS Sync]
    end

    subgraph Pipeline 4: Lead Routing & Territory Assignment
        A4[Qualified Lead Ingest] --> B4[Draft 2020-12 Schema Validation]
        B4 --> C4[Territory & Segment Resolver]
        C4 --> D4[Enterprise AE / Regional AM / SMB Round-Robin Queues]
    end

    subgraph Pipeline 5: Deal Desk & Discount Approval
        A5[Quote Approval Request] --> B5[Draft 2020-12 Schema Validation]
        B5 --> C5[Discount & Governance Matrix]
        C5 --> D5[Auto-Approve / VP Sales / Deal Desk CFO Escalation]
    end
