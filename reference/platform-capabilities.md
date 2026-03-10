# Platform & Product Capabilities - Reference

> **Last reviewed:** 2026-03

Reference material for Salesforce products, features, editions, AI, and automation.

## Product Overview

### Stable URLs
- https://www.salesforce.com/products/
- https://www.salesforce.com/editions-pricing/overview/

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
- https://developer.salesforce.com/docs/atlas.en-us.c360a_api.meta/c360a_api/c360a_api_quick_start.htm

### Search Queries
- "Data Cloud overview site:help.salesforce.com"

## Agentforce & AI

### Stable URLs
- https://www.salesforce.com/agentforce/
- https://developer.salesforce.com/docs/einstein/genai/overview

### Search Queries
- "Agentforce copilot overview site:help.salesforce.com"
- "Einstein Trust Layer generative AI site:help.salesforce.com"

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
- https://developer.salesforce.com/docs/component-library/overview/components
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
| Agentforce autonomous AI agents | Yes | Act on CRM data across channels |
| Einstein predictive AI (lead scoring, forecasting) | Yes | Built into Sales and Service Clouds |
| Einstein generative AI (content, summaries) | Yes | Trust Layer governs all AI interactions |
| Einstein Trust Layer | Yes | Prompt defense, data masking, toxicity detection, audit trail |
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
