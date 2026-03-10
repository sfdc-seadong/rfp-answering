# Data 360 & CDP - Reference

> **Last reviewed:** 2026-03

Reference material for Salesforce Data 360 (formerly Data Cloud / Customer Data Platform), including segmentation, identity resolution, activation, connectors, zero-copy data sharing, and platform limits.

## Data 360 Overview

### Stable URLs
- https://www.salesforce.com/data/

### Search Queries
- "Data Cloud overview site:help.salesforce.com"
- "Data Cloud solution kits site:help.salesforce.com"

## Data Streams & Ingestion

### Stable URLs
- https://developer.salesforce.com/docs/data/data-cloud-ref/guide/c360a-api-get-started.html
- https://developer.salesforce.com/docs/data/data-cloud-ref/guide

### Search Queries
- "Data Cloud data streams ingestion site:help.salesforce.com"

## Data Model Objects (DMOs) & Data Mapping

### Stable URLs
- https://developer.salesforce.com/docs/data/data-cloud-ref/guide/c360a-api-isv-readiness-data.html

### Search Queries
- "Data Cloud data model objects DMO site:help.salesforce.com"
- "Data Cloud data mapping site:help.salesforce.com"

## Identity Resolution

### Stable URLs
- https://trailhead.salesforce.com/content/learn/projects/quick-start-create-identity-resolution-ruleset
- https://trailhead.salesforce.com/content/learn/projects/quick-start-create-identity-resolution-ruleset/get-started-with-identity-resolution-ruleset

### Search Queries
- "Data Cloud identity resolution site:help.salesforce.com"
- "Data Cloud identity resolution segments site:help.salesforce.com"

## Unified Individual Profile

### Search Queries
- "Data Cloud unified individual profile site:help.salesforce.com"
- "Data Cloud profile explorer site:help.salesforce.com"

## Segmentation

### Stable URLs
- https://trailhead.salesforce.com/content/learn/projects/quick-start-create-a-data-cloud-segment/create-and-activate-a-segment-in-data-cloud
- https://trailhead.salesforce.com/content/learn/modules/data-cloud-query-and-segment/run-queries-and-personalize-engagement-with-segmentation
- https://trailhead.salesforce.com/content/learn/projects/explore-data-cloud-core-functionality/build-a-segment-and-report

### Search Queries
- "Data Cloud segmentation create segment site:help.salesforce.com"
- "Data Cloud segment builder interface site:help.salesforce.com"

## Activation & Activation Targets

### Search Queries
- "Data Cloud activation segment site:help.salesforce.com"
- "Data Cloud activation targets site:help.salesforce.com"
- "Data Cloud add activation target site:help.salesforce.com"

## Activation Framework & Custom Targets

### Search Queries
- "Data Cloud connector framework site:help.salesforce.com"
- "Data Cloud connector list site:help.salesforce.com"

## Real-Time / Streaming Ingestion & Activation

### Stable URLs
- https://developer.salesforce.com/docs/data/data-cloud-int/references/data-cloud-ingestionapi-ref/c360-a-real-time-ingestion-api.html
- https://developer.salesforce.com/docs/data/data-cloud-int/guide/c360-a-create-eventbusconnector-data-stream.html
- https://developer.salesforce.com/docs/data/data-cloud-int/guide/c360-a-mobile-web-datastream.html
- https://developer.salesforce.com/blogs/2024/08/automate-your-workflow-with-data-cloud-triggered-flows-and-invocable-actions

## Calculated Insights

### Stable URLs
- https://developer.salesforce.com/docs/data/data-cloud-ref/guide/c360a-api-calculated-insights.html

### Search Queries
- "Data Cloud calculated insights site:help.salesforce.com"

## Zero-Copy Data Sharing

### Stable URLs
- https://trailhead.salesforce.com/content/learn/modules/data-cloud-with-zero-copy/get-started-with-zero-copy-data-sharing
- https://developer.salesforce.com/blogs/2024/08/zero-copy-data-federation-with-snowflake-and-salesforce-data-cloud

### Search Queries
- "Data Cloud zero-copy data sharing site:help.salesforce.com"

## Connectors

### Search Queries
- "Data Cloud connector list site:help.salesforce.com"
- "Data Cloud connect S3 site:help.salesforce.com"
- "Data Cloud connect GCS Azure site:help.salesforce.com"

## Data 360 + Agentforce

### Stable URLs
- https://www.salesforce.com/agentforce/
- https://developer.salesforce.com/docs/einstein/genai/overview

### Search Queries
- "Data Cloud Agentforce copilot site:help.salesforce.com"

## Data 360 Limits & Guidelines

### Stable URLs
- https://developer.salesforce.com/docs/data/data-cloud-ref/guide

### Search Queries
- "Data Cloud limits guidelines site:help.salesforce.com"

## Data 360 APIs

### Stable URLs
- https://developer.salesforce.com/docs/atlas.en-us.c360a_api.meta/c360a_api/c360a_api_quick_start.htm
- https://developer.salesforce.com/docs/data/data-cloud-ref/guide/c360a-api-get-started.html

## Trailhead Learning Paths

### Stable URLs
- https://trailhead.salesforce.com/content/learn/trails/get-started-with-data-cloud
- https://trailhead.salesforce.com/content/learn/modules/data-cloud-quick-look

## Key Native Capabilities (Quick Reference)

When reference URLs fail or return thin results, use this section as a floor. These capabilities are **natively built into Data 360** and should never be described as requiring custom build, manual workarounds, or external tools. Do not undersell them.

### Segmentation — Native

| Capability | Native? | Notes |
|---|---|---|
| Waterfall / priority-based segmentation | **Yes — fully native** | Segments are evaluated in defined priority order. Customers are assigned to the highest-priority segment they qualify for and automatically excluded from lower-priority segments. This IS how mutually exclusive segments work. |
| Segment splits (% or random) | **Yes — native** | Segments can be split into sub-groups by percentage or random assignment for testing and experimentation. |
| Segment merging (union, intersection, exclusion) | **Yes — native** | The segment builder supports combining segments using logical operations (AND/OR/NOT, include/exclude). |
| Include/exclude existing segments in new segments | **Yes — native** | Existing segments can be referenced as inclusion or exclusion criteria within new segment definitions. |
| SQL-based segmentation | **Yes — native** | Full SQL access for segment creation via calculated insights and streaming insights. Supports JOINs, WHERE, GROUP BY, aggregation, and custom expressions. |
| No-code visual query builder | **Yes — native** | Drag-and-drop segment builder with boolean logic (AND/OR/NOT), nested conditions, and attribute filtering. No SQL required. |
| Streaming / near-real-time segments | **Yes — native** | Streaming insights process real-time data from engagement sources. Segments can refresh on streaming cadence. |
| Static segment import | **Yes — native** | Pre-built segments can be imported via file ingestion (CSV, S3, GCS, Azure, SFTP). |
| Calculated insights (computed attributes) | **Yes — native** | SQL-defined metrics and aggregations that create new attributes on unified profiles. Used for RFM, scoring, and derived attributes. |
| Einstein Segment Creation (AI-assisted) | **Yes — native** | Natural-language segment creation using AI, enriched by Einstein Data Prism semantic layer. |

### Identity Resolution — Native

| Capability | Native? | Notes |
|---|---|---|
| Deterministic matching (exact match on identifiers) | **Yes — native** | Match on email, phone, CRM ID, device ID, or any custom identifier. |
| Probabilistic / fuzzy matching (AI-powered) | **Yes — native** | ML-powered soft matching handles nicknames, initials, cross-cultural spellings, gender variants. Configurable confidence thresholds (low/medium/high precision). |
| Configurable match rulesets | **Yes — native** | Organizations define which identifiers participate, set priority hierarchies, and control reconciliation rules. |
| Multiple identity levels (Individual, Household, Account) | **Yes — native** | Users can switch between ID levels in segmentation. Household and account grouping supported. |
| Unified Individual profile with identity graph | **Yes — native** | Profile explorer shows all linked identifiers, source records, and identity graph structure. |
| Universal ID Lookup API | **Yes — native** | Programmatic lookup of all records associated with a unified profile. |

### Activation — Native

| Capability | Native? | Notes |
|---|---|---|
| Identity resolution on egress | **Yes — native** | Unified profiles are resolved to destination-specific identifiers during activation. This is automatic, not manual. |
| Pre-built ad platform connectors | **Yes — GA:** Google Ads, Meta Ads, The Trade Desk. **Beta:** Snapchat Ads, LinkedIn Ads. | These are outbound activation targets, not just inbound data connectors. |
| File-based activation (S3, GCS, Azure, SFTP) | **Yes — native** | Audiences activated to cloud storage or SFTP for any downstream platform that accepts file ingestion. |
| Activation-triggered Flows | **Yes — native** | Flows auto-trigger when segments publish or DMOs activate. Enables code-free activation to any HTTP API endpoint. Verify GA status against current release notes. |
| Salesforce CRM activation | **Yes — native** | Direct, bi-directional activation into Sales Cloud, Service Cloud, Marketing Cloud — no middleware required. |
| Activation scheduling and monitoring | **Yes — native** | Configurable refresh cadences, delivery status dashboards, and volume monitoring. |

### Data Ingestion — Native

| Capability | Native? | Notes |
|---|---|---|
| 200+ pre-built connectors | **Yes — native** | Connectors span CRMs, ad platforms, databases, cloud storage, marketing tools. |
| Zero-copy data sharing | **Yes — native** | Bidirectional data access with Snowflake, Databricks, BigQuery, Amazon Redshift — no data movement. |
| Streaming Ingestion API | **Yes — native** | Near-real-time event processing. Verify current latency benchmarks against latest release notes. |
| AWS S3 and Redshift connectors | **Yes — native** | S3 for file-based ingestion. Redshift via zero-copy federation with IDP-based auth. |
| Web SDK / Mobile SDK | **Yes — native** | Client-side data collection for engagement and profile data. |
| Data quality and validation rules | **Yes — native** | Data mapping layer applies validation, standardization, and normalization during ingestion. |

### Reporting & Analytics — Native

| Capability | Native? | Notes |
|---|---|---|
| Segment size and membership tracking | **Yes — native** | Built-in segment analytics show size, composition, and membership over time. |
| Profile attribute analytics | **Yes — native** | Profile explorer and analytics surface attribute distributions and value breakdowns. |
| Identity resolution reporting (match rates) | **Yes — native** | Identity resolution dashboard shows match rates, linked identifiers, and profile stitching outcomes. |
| One-click reporting on DMOs and insights | **Yes — native** | Reports can be created directly from calculated insights and DMO list views. |

### Data Governance & Observability — Native

| Capability | Native? | Notes |
|---|---|---|
| Unified Lineage (object-level and field-level) | **Yes — native, auto-enabled** | Visual relationship graph showing how data objects are connected from source through activation. Field-level lineage covers DLOs, data transforms, DMOs, CIs, segments, activations, identity resolutions, data graphs, and data shares. Object-level lineage additionally covers data streams, connection info, semantic data models, and unstructured objects. No setup required — automatically enabled in all orgs. URL: `https://help.salesforce.com/s/articleView?language=en_US&id=data.c360_a_viewing_data_lineage.htm&type=5` |
| Data Cloud Jobs monitoring | **Yes — native** | Dedicated monitoring console for Data Cloud-specific jobs: data stream ingestion, identity resolution, segment refresh, activation publish. Shows status, timing, record counts, errors. This is NOT the core platform jobs page — it is DC-specific. URL: `https://help.salesforce.com/s/articleView?id=xcloud.data_monitoring_jobs.htm&language=en_US&type=5` |
| Downstream impact analysis (automated) | **No — manual navigation** | Unified Lineage shows field-level dependencies visually, but there is no automated "click a field and see all affected segments/activations" feature. Administrators trace dependencies by navigating the lineage graph. Do NOT describe this as automated one-click impact analysis. Score 3 on questions about automated impact analysis. |

## Search Fallback

If none of the above cover a specific Data 360 question, search:
`"Data Cloud [topic] site:help.salesforce.com"` or `"Data 360 [topic] site:developer.salesforce.com"` or `"Customer Data Platform [topic] site:salesforce.com"`
