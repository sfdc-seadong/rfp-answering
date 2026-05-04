# Platform & Product Capabilities - Reference

> **Last reviewed:** 2026-04

Reference material for Salesforce products, features, editions, AI, and automation.

## Product Overview

### Stable URLs
- https://www.salesforce.com/products/
- https://www.salesforce.com/pricing/

## Sales Cloud

### Stable URLs
- https://www.salesforce.com/sales/

### Search Queries
- "Sales Cloud overview site:help.salesforce.com"
- "CPQ overview site:help.salesforce.com"

## Service Cloud

### Stable URLs
- https://www.salesforce.com/service/

### Search Queries
- "Service Cloud overview agents site:help.salesforce.com"
- "Field Service overview site:help.salesforce.com"

## Service Cloud Voice

### Stable URLs
- https://developer.salesforce.com/docs/atlas.en-us.voice_developer_guide.meta/voice_developer_guide/voice_intro.htm

### Search Queries
- "Service Cloud Voice overview site:help.salesforce.com"
- "Service Cloud Voice setup recordings site:help.salesforce.com"

## Marketing Cloud & Account Engagement

### Stable URLs
- https://www.salesforce.com/marketing/

### Search Queries
- "Account Engagement Pardot overview site:help.salesforce.com"

## Commerce Cloud

### Stable URLs
- https://www.salesforce.com/commerce/
- https://developer.salesforce.com/docs/commerce/salesforce-commerce/overview

## Experience Cloud

### Search Queries
- "Experience Cloud communities overview site:help.salesforce.com"

## Data 360

### Stable URLs
- https://www.salesforce.com/data/
- https://developer.salesforce.com/docs/data/data-cloud-ref/guide/c360a-api-quick-start.html

### Search Queries
- "Data Cloud overview site:help.salesforce.com"

## Agentforce & AI

### Stable URLs
- https://www.salesforce.com/agentforce/
- https://developer.salesforce.com/docs/ai/agentforce/overview
- https://developer.salesforce.com/docs/ai/agentforce/guide/agent-script.html
- https://github.com/salesforce/agent-script

### Search Queries
- "Agentforce copilot overview site:help.salesforce.com"
- "Einstein Trust Layer generative AI site:help.salesforce.com"
- "Agent Script Agentforce site:developer.salesforce.com"

## Agent Script

### Stable URLs
- https://developer.salesforce.com/docs/ai/agentforce/guide/agent-script.html
- https://github.com/salesforce/agent-script

### Search Queries
- "Agent Script open source site:developer.salesforce.com"
- "Agent Script language Agentforce site:salesforce.com"

### Key Details

Agent Script is an **open-source agent definition language** announced at TDX (April 2026). It lets developers specify when agents should use LLM reasoning versus deterministic logic.

| Feature | Details |
|---|---|
| Open source | Full language specification, grammar, parser, and compiler on GitHub |
| Deterministic control | If-then-else conditions, transitions, variable management — predictable workflows without relying solely on LLM |
| Sub-agents and actions | Compose agents from smaller sub-agents with defined actions, variables, guardrails, and transitions |
| Platform dialects | Base language with platform-specific extensions (like SQL) — Agentforce dialect and MuleSoft Agent Fabric dialect |
| AI-native authoring | Designed to be written by coding agents (Claude Code, Cursor, Codex) as well as manually by developers |
| Strongly typed | Structured, strongly-typed files for reliability and validation |

## Agentforce Labs & ADLC

### Stable URLs
- https://github.com/SalesforceAIResearch/agentforce-adlc

### Key Details

**Agentforce Labs** (announced TDX April 2026): Incubation program for agent development. Ships experiments, tests with real developers, and graduates successful innovations to core Agentforce or retires them.

**ADLC (Agent Development Lifecycle)**: Skills that close the loop from IDE to production:
- Authoring, discovery, scaffolding, deployment, testing, and optimization
- LLM-driven safety reviews across 7 categories
- Session trace analysis for data-driven agent optimization

## Einstein AI (Predictive & Generative)

### Stable URLs
- https://www.salesforce.com/artificial-intelligence/

### Search Queries
- "Einstein AI overview site:help.salesforce.com"

## Automation (Flow, MuleSoft)

### Stable URLs
- https://www.mulesoft.com/platform/enterprise-integration

### Search Queries
- "Flow automation overview site:help.salesforce.com"
- "OmniStudio overview site:help.salesforce.com"

## AppExchange

### Stable URLs
- https://appexchange.salesforce.com/

### Search Queries
- "AppExchange overview site:help.salesforce.com"

## Platform & Development

### Stable URLs
- https://developer.salesforce.com/docs
- https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_intro.htm
- https://developer.salesforce.com/docs/platform/lightning-component-reference/guide
- https://architect.salesforce.com/

## Mobile

### Search Queries
- "Salesforce mobile app overview site:help.salesforce.com"

## Release Notes (Latest)

### Search Queries
- "Salesforce release notes site:help.salesforce.com"

## Key Native Capabilities

When reference URLs fail or return thin results, use this section as a fallback. These capabilities are natively available on the Salesforce platform and should not be described as requiring custom build or external tools.

| Capability | Native? | Notes |
|---|---|---|
| Multi-cloud CRM (Sales, Service, Marketing, Commerce) | Yes | Included by edition |
| Flow automation (no-code/low-code) | Yes | Declarative process automation |
| Apex custom logic | Yes | Server-side code execution |
| Lightning Web Components (LWC) | Yes | Custom UI development framework |
| Agentforce autonomous AI agents | Yes | Act on CRM data across channels; ~29,000 deals closed, ~$800M ARR as of early 2026 |
| Einstein predictive AI (lead scoring, forecasting) | Yes | Built into Sales and Service Clouds |
| Einstein generative AI (content, summaries) | Yes | Trust Layer governs all AI interactions |
| Einstein Trust Layer | Yes | Prompt defense, data masking, toxicity detection, audit trail |
| Agent Script (open-source agent language) | Yes | Define agent behavior with deterministic + LLM logic; platform dialects for Agentforce and MuleSoft |
| Agentforce Labs (incubation program) | Yes | Experimental agent development features; ships prototypes, tests with developers |
| ADLC (Agent Development Lifecycle) | Yes | Full IDE-to-production lifecycle for agent authoring, testing, and deployment |
| AppExchange marketplace | Yes | 5,000+ pre-built apps and components |
| OmniStudio guided experiences | Yes | Included in select editions |
| Experience Cloud portals/communities | Yes | Customer and partner portals |
| Mobile app | Yes | Native iOS/Android with offline support |
| Service Cloud Voice (call recording, transcription) | Yes | Telephony integration; recording/storage handled by telephony provider (e.g., Amazon Connect) |
| Three major releases per year | Yes | Spring, Summer, Winter with preview sandboxes |

## Marketing Optimization Capabilities

When reference URLs fail or return thin results, use this section as a fallback. Pay close attention to what each feature does and does NOT do — these are commonly overscored.

| Capability | Native? | Notes |
|---|---|---|
| Einstein Engagement Frequency (EEF) | **Yes — native** | Segments contacts into Saturated / Almost Saturated / On Target / Undersaturated based on 28-day engagement patterns. Available as a Journey Builder split activity. This is **frequency optimization** (should I send to this person?), NOT message prioritization (which message should I send?). Do NOT conflate with cross-journey prioritization. |
| Einstein Engagement Scoring (EES) | **Yes — native** | Per-contact predictive scores for open, click, subscribe, and convert likelihood. Used in journey decision splits to inform targeting. This is **engagement prediction**, NOT cross-journey priority resolution. |
| Path Optimizer | **Yes — native** | A/B tests up to 10 journey path variants and auto-routes to the winner. Operates **within a single journey only** — does NOT arbitrate across journeys. |
| Einstein Send Time Optimization (ESTO) | **Yes — native** | Predicts optimal send time per contact. Per-journey, not cross-journey. |
| Cross-journey message prioritization | **No — does not exist natively** | No centralized engine determines which of multiple competing campaigns takes precedence for a given customer. Must be implemented via segment exclusion logic and manual campaign hierarchy design. Score 3 on questions about this capability. Never describe it as automatic or native. |

## Search Fallback

If none of the above cover a specific product question, search:
`"[product name] site:help.salesforce.com"` or `"[product name] site:developer.salesforce.com"`
