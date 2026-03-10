# Architecture & Infrastructure - Reference

> **Last reviewed:** 2026-03

Reference material for Salesforce architecture, multi-tenancy, uptime, disaster recovery, data centers, and scalability.

## Architecture Overview

### Stable URLs
- https://architect.salesforce.com/
- https://architect.salesforce.com/fundamentals/platform-multitenant-architecture
- https://developer.salesforce.com/docs/atlas.en-us.fundamentals.meta/fundamentals/adg_preface.htm

## Multi-Tenant Architecture

### Stable URLs
- https://architect.salesforce.com/fundamentals/platform-multitenant-architecture

### Search Queries
- "governor limits overview site:help.salesforce.com"

## Hyperforce (Public Cloud Infrastructure)

### Stable URLs
- https://www.salesforce.com/hyperforce/

### Search Queries
- "Hyperforce overview site:help.salesforce.com"

## Trust & Uptime

### Stable URLs
- https://trust.salesforce.com/en/
- https://trust.salesforce.com/en/status/
- https://trust.salesforce.com/en/trust-and-compliance-documentation/

## Disaster Recovery & Business Continuity

### Stable URLs
- https://trust.salesforce.com/en/security/disaster-recovery/
- https://www.salesforce.com/products/backup-recovery/

### Search Queries
- "data export service site:help.salesforce.com"

## Sandboxes

### Search Queries
- "sandbox environments overview site:help.salesforce.com"
- "deploy sandboxes site:help.salesforce.com"

## Governor Limits

### Stable URLs
- https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_gov_limits.htm
- https://developer.salesforce.com/docs/atlas.en-us.salesforce_app_limits_cheatsheet.meta/salesforce_app_limits_cheatsheet/

## Release Management

### Stable URLs
- https://www.salesforce.com/blog/salesforce-release-schedule/

### Search Queries
- "Salesforce release notes site:help.salesforce.com"

## Performance & Scalability

### Stable URLs
- https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_limits.htm

### Search Queries
- "large data volumes performance site:help.salesforce.com"

## Architecture Decision Guides

### Stable URLs
- https://architect.salesforce.com/decision-guides/
- https://architect.salesforce.com/decision-guides/data-architecture
- https://architect.salesforce.com/decision-guides/security

## Key Native Capabilities

When reference URLs fail or return thin results, use this section as a fallback. These capabilities are natively available and should not be described as requiring custom build or external tools.

| Capability | Native? | Notes |
|---|---|---|
| Multi-tenant architecture | Yes | Logical data isolation per org |
| Hyperforce (public cloud deployment) | Yes | Customer-selected geographic regions |
| 99.9%+ uptime SLA | Yes | Contractual commitment |
| Real-time data replication (DR) | Yes | Synchronous replication across data centers |
| Near-zero RPO | Yes | Core transactional data |
| RTO ≤ 4 hours | Yes | Target recovery time |
| Sandbox environments (Developer, Partial, Full) | Yes | Included by edition |
| Governor limits | Yes | Fair resource allocation across tenants |
| Zero-downtime upgrades | Yes | Three major releases per year |
| Large data volume support | Yes | Big objects, async processing, skinny tables |
| Data export service | Yes | Scheduled CSV exports |
| Salesforce Backup (automated daily) | Yes (add-on) | Self-service restore |

## Search Fallback

If none of the above cover a specific architecture question, search:
`"[topic] site:architect.salesforce.com"` or `"[topic] architecture site:help.salesforce.com"`
