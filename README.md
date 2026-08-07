# Enterprise RevOps Architecture Portfolio

Master architecture repository for production-ready Revenue Operations automation pipelines. This organization contains event-driven systems built around strict JSON Schema contracts, deterministic JavaScript scoring modules, and n8n workflow orchestration.

---

## System Architecture

```mermaid
flowchart TD
    classDef engine fill:#1e1e2e,stroke:#89b4fa,stroke-width:2px,color:#cdd6f4;
    classDef step fill:#313244,stroke:#a6adc8,stroke-width:1px,color:#cdd6f4;

    subgraph P1["1. Campaign Content Production Engine"]
        A1[Campaign Brief Payload] --> B1[Draft 2020-12 Schema Validation]
        B1 --> C1[Multi-Agent Content Execution]
        C1 --> D1[n8n Campaign Publishing Workflow]
    end

    subgraph P2["2. Lead Enrichment & Scoring Pipeline"]
        A2[Inbound Lead Event] --> B2[Draft 2020-12 Schema Validation]
        B2 --> C2[Parallel Firmographic & Technographic Enrichment]
        C2 --> D2[0-100 Deterministic Matrix Scoring]
        D2 --> E2[Tier 1 MQL / Tier 2 SQL / Tier 3 Nurture / DLQ]
    end

    subgraph P3["3. Churn & Expansion Intelligence Engine"]
        A3[Account Telemetry Event] --> B3[Draft 2020-12 Schema Validation]
        B3 --> C3[Contract Metadata Aggregator]
        C3 --> D3[0-100 Account Health Matrix Engine]
        D3 --> E3[Slack Risk Alert / Expansion Opportunity / CS Sync]
    end

    subgraph P4["4. Lead Routing & Territory Assignment Engine"]
        A4[Qualified Lead Ingest] --> B4[Draft 2020-12 Schema Validation]
        B4 --> C4[Territory & Segment Resolver]
        C4 --> D4[Enterprise AE / Regional AM / SMB Round-Robin Queues]
    end

    subgraph P5["5. Deal Desk & Discount Approval Engine"]
        A5[Quote Approval Request] --> B5[Draft 2020-12 Schema Validation]
        B5 --> C5[Discount & Governance Matrix]
        C5 --> D5[Auto-Approve / VP Sales / Deal Desk CFO Escalation]
    end

    P1 --> P2 --> P4 --> P5 --> P3

    class P1,P2,P3,P4,P5 engine;
    class A1,B1,C1,D1,A2,B2,C2,D2,E2,A3,B3,C3,D3,E3,A4,B4,C4,D4,A5,B5,C5,D5 step;
