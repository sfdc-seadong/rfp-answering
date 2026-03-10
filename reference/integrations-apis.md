# Integrations & APIs - Reference

> **Last reviewed:** 2026-03

Reference material for Salesforce APIs, integration patterns, SSO, MuleSoft, and connectors.

## API Overview

### Stable URLs
- https://developer.salesforce.com/docs/apis
- https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_rest.htm

## REST API

### Stable URLs
- https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_rest.htm
- https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_limits.htm

## SOAP API

### Stable URLs
- https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_quickstart_intro.htm

## Bulk API 2.0

### Stable URLs
- https://developer.salesforce.com/docs/atlas.en-us.api_asynch.meta/api_asynch/api_asynch_introduction_bulk_api.htm

## GraphQL API

### Stable URLs
- https://developer.salesforce.com/docs/platform/graphql/overview

## Streaming & Event-Driven

### Stable URLs
- https://developer.salesforce.com/docs/atlas.en-us.api_streaming.meta/api_streaming/intro_stream.htm
- https://developer.salesforce.com/docs/platform/platform-events/overview
- https://developer.salesforce.com/docs/atlas.en-us.change_data_capture.meta/change_data_capture/cdc_intro.htm
- https://developer.salesforce.com/docs/platform/pub-sub-api/overview

## Metadata API

### Stable URLs
- https://developer.salesforce.com/docs/atlas.en-us.api_meta.meta/api_meta/meta_intro.htm

## MuleSoft

### Stable URLs
- https://www.mulesoft.com/platform/enterprise-integration
- https://www.mulesoft.com/exchange/
- https://docs.mulesoft.com/salesforce-connector/latest/

## MuleSoft Composer (No-Code)

### Search Queries
- "MuleSoft Composer overview site:help.salesforce.com"

## Salesforce Connect (External Objects)

### Search Queries
- "Salesforce Connect external objects site:help.salesforce.com"

## SSO & Identity

### Search Queries
- "SSO single sign-on SAML site:help.salesforce.com"
- "identity provider overview site:help.salesforce.com"
- "authentication providers site:help.salesforce.com"

## OAuth & Connected Apps

### Search Queries
- "connected app overview OAuth site:help.salesforce.com"
- "OAuth authorization flows site:help.salesforce.com"

## Named Credentials

### Search Queries
- "named credentials overview site:help.salesforce.com"

## SCIM (User Provisioning)

### Search Queries
- "SCIM user provisioning overview site:help.salesforce.com"

## Integration Patterns (Architecture)

### Stable URLs
- https://architect.salesforce.com/decision-guides/integration-architecture
- https://developer.salesforce.com/docs/atlas.en-us.integration_patterns_and_practices.meta/integration_patterns_and_practices/

## API Limits Reference

### Stable URLs
- https://developer.salesforce.com/docs/atlas.en-us.salesforce_app_limits_cheatsheet.meta/salesforce_app_limits_cheatsheet/

## Key Native Capabilities

When reference URLs fail or return thin results, use this section as a fallback. These capabilities are natively available and should not be described as requiring custom build or external tools.

| Capability | Native? | Notes |
|---|---|---|
| REST API | Yes | JSON-based CRUD and query |
| SOAP API | Yes | XML/WSDL-based |
| Bulk API 2.0 | Yes | Async CSV for large data volumes (up to 150M records/day) |
| GraphQL API | Yes | Flexible query language |
| Streaming API (CometD) | Yes | Real-time event notifications |
| Pub/Sub API (gRPC) | Yes | Change Data Capture and Platform Events |
| Change Data Capture | Yes | Granular create/update/delete events |
| Platform Events | Yes | Custom event-driven architecture |
| Metadata API | Yes | Programmatic deployment and configuration |
| Tooling API | Yes | Developer tooling and debugging |
| Salesforce Connect (external objects) | Yes | Live access to external data without ETL |
| Named Credentials | Yes | Secure callout authentication management |
| MuleSoft integration middleware | Yes (add-on) | Enterprise integration platform with 400+ connectors |
| MuleSoft Composer (no-code) | Yes (add-on) | Point-and-click integration builder |
| Connected Apps / OAuth | Yes | Secure third-party app authentication |

## Search Fallback

If none of the above cover a specific integration question, search:
`"[topic] site:developer.salesforce.com"` or `"[topic] integration site:help.salesforce.com"`
