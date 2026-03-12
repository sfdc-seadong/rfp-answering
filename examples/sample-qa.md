# Sample RFP Q&A Pairs

These examples calibrate tone, length, and style for RFP responses. Use them as a reference when drafting answers. Answer length and Sources follow [format-defaults.md](../reference/format-defaults.md).

**All examples below use the default "no product names" mode** — generic terms replace Salesforce product names per the mapping in SKILL.md. For product-names-mode examples, see the [Product Names Mode](#product-names-mode-examples) section at the bottom.

## Standard Format Examples

---

### Q1: Describe your platform's multi-tenant architecture and how customer data is isolated.

**Answer:** The platform operates a multi-tenant architecture where all customers share the same infrastructure and application code, but data is logically isolated at the organization (org) level.

Each customer receives a unique OrgId. Data access is enforced at every layer: database queries are automatically scoped to the requesting org, API calls are authenticated per-org, and governor limits ensure fair resource allocation. No customer can access another customer's data through the platform. This architecture has been in production for over 20 years and serves 150,000+ organizations globally.

**Review:** Auto-approved
**Sources:**
- https://architect.salesforce.com/fundamentals/platform-multitenant-architecture
- https://help.salesforce.com/s/articleView?id=sf.overview_limits_general.htm

---

### Q2: How does your platform handle data encryption at rest and in transit?

**Answer:** All data at rest is encrypted using AES-256 across the platform's infrastructure. All data in transit is protected with TLS 1.2 or higher with Perfect Forward Secrecy.

For customers with heightened encryption requirements, an add-on encryption service provides field-level encryption with customer-managed keys (Bring Your Own Key). This allows customers to encrypt specific sensitive fields (e.g., SSN, financial data, health records) with keys they control, while maintaining the ability to search and filter on deterministically encrypted fields. Key rotation and tenant secret management are handled through the platform's HSM-backed key management infrastructure.

**Review:** Auto-approved
**Sources:**
- https://help.salesforce.com/s/articleView?id=sf.security_pe_overview.htm
- https://help.salesforce.com/s/articleView?id=sf.security_encryption_at_rest.htm

---

### Q3: What APIs are available for integration, and what are the rate limits?

**Answer:** A comprehensive API suite is available: REST API (JSON), SOAP API (XML/WSDL), Bulk API 2.0 (async CSV for large data volumes), Streaming API (real-time events via CometD), GraphQL API, Metadata API, Pub/Sub API (gRPC), and Tooling API.

API rate limits vary by edition. Enterprise Edition includes 15,000 REST/SOAP API calls per 24-hour period. Performance and Unlimited Editions offer higher limits. Bulk API supports up to 15,000 batches per 24 hours and can process up to 150 million records per day. Streaming API supports 2,000 concurrent clients. These limits can be increased through add-on API call packs.

**Review:** Auto-approved
**Sources:**
- https://developer.salesforce.com/docs/apis
- https://developer.salesforce.com/docs/atlas.en-us.salesforce_app_limits_cheatsheet.meta/salesforce_app_limits_cheatsheet/

---

### Q4: What SSO and identity federation options are supported?

**Answer:** SAML 2.0 and OpenID Connect are supported for single sign-on, and the platform can function as either an Identity Provider (IdP) or Service Provider (SP).

Additional identity capabilities include: Just-in-Time (JIT) user provisioning, SCIM 2.0 for automated user lifecycle management (provisioning and deprovisioning), OAuth 2.0 for API authentication, custom login URLs via domain configuration, and social sign-on (Google, Apple, Facebook). For customers using a third-party IdP (Okta, Azure AD, Ping Identity, etc.), the platform integrates as a SAML SP with delegated authentication.

**Review:** Auto-approved
**Sources:**
- https://help.salesforce.com/s/articleView?id=sf.sso_about.htm
- https://help.salesforce.com/s/articleView?id=sf.identity_overview.htm

---

### Q5: How does your AI/ML offering work and what safeguards exist?

**Answer:** Built-in AI capabilities span predictive AI (lead scoring, forecasting), generative AI (content generation, summarization), and autonomous AI agents that act across sales, service, and marketing workflows.

All AI features operate within a dedicated trust layer that provides: prompt defense (injection detection), data masking of sensitive fields before LLM processing, toxicity detection on outputs, a full audit trail of AI interactions, and data grounding using only the customer's CRM data. The trust layer ensures no customer data is used to train the vendor's AI models. Customers can also bring their own models (BYOM) via a model builder for custom predictions.

**Review:** Auto-approved
**Sources:**
- https://help.salesforce.com/s/articleView?id=sf.generative_ai_trust_layer.htm
- https://www.salesforce.com/artificial-intelligence/

---

## Concise Format Examples

The concise format combines the answer and supporting detail into 2-3 dense sentences. Use when the user requests brevity. Sources always cite live URLs, with official docs listed before blog links.

---

### Q: How does the platform integrate with external data sources for campaign data enrichment?

**Answer:** The CDP provides 200+ pre-built connectors spanning advertising platforms, marketing automation tools, commerce systems, databases, cloud storage, and analytics services to ingest external data via batch, streaming, or zero-copy methods — including bidirectional, real-time access to data in Snowflake, Databricks, Google BigQuery, and Amazon Redshift without duplication or ETL pipelines. Once ingested, identity resolution unifies customer profiles across all sources, enabling dynamic audience segmentation and activation to advertising and marketing channels for enriched campaign targeting.

**Review:** Auto-approved
**Sources:**
- https://developer.salesforce.com/docs/data/data-cloud-int/guide/c360-a-thirdparty-connectors.html
- https://www.salesforce.com/data/
- https://www.salesforce.com/data/zero-copy-partner-network/guide/

---

### Q: How does AI extract structured data from call transcriptions and auto-populate fields?

**Answer:** The platform automatically transcribes voice and video calls, then applies generative AI to extract key data points — such as competitor mentions, customer objections, pricing sentiment, next steps, and deal stage changes — and surfaces them directly on relevant CRM records. AI agents can synthesize these conversation insights into structured field updates either autonomously or in a suggestive mode, while configurable extraction schemas allow structured information to be pulled from any unstructured source and auto-populated into CRM fields via automation workflows.

**Review:** Auto-approved
**Sources:**
- https://salesforce.com/sales/conversation-intelligence
- https://www.salesforce.com/blog/sales-cloud-product-release/
- https://developer.salesforce.com/blogs/2025/09/integrate-data-clouds-document-ai-with-agentforce

---

### Q: Can your platform integrate with Azure Cosmos DB for MDM provider profiles (read, write, change feed)?

**Answer:** A native Azure Cosmos DB connector supports structured data ingestion (data-in) via batch processing, enabling read of Cosmos DB data into unified profiles for MDM use cases. The connector is currently in beta and supports data-in direction only; for bidirectional write-back and change feed scenarios, the platform's REST and Bulk APIs, automation workflows, and native integration middleware connectors can push updates back to Cosmos DB, and third-party integration platforms (e.g., Estuary Flow, Striim) provide real-time CDC with sub-100ms latency for continuous bidirectional synchronization.

**Review:** SME Review
_Internal note: Verify (1) GA timeline for the Azure Cosmos DB connector, (2) bidirectional and change feed roadmap, (3) recommended MDM write-back architecture._

**Sources:**
- https://developer.salesforce.com/docs/data/data-cloud-int/guide/c360-a-azurecosmosdb-connector.html
- https://developer.salesforce.com/docs/data/data-cloud-int/guide/c360-a-create-azurecosmosdb-data-stream.html

---

### Q: How does your platform support bi-directional data synchronization (real-time, batch, conflict resolution)?

**Answer:** Bidirectional synchronization is supported through multiple mechanisms: real-time ingestion via streaming APIs (with 95% of events processed end-to-end within ~500ms), batch ingestion through 200+ connectors and bulk APIs (CSV-based, scheduled), and zero-copy federation that enables bidirectional read/write access to external warehouses (Snowflake, Databricks, BigQuery, Redshift) without physically moving data. For outbound sync, Change Data Capture publishes granular create/update/delete events via a gRPC-based Pub/Sub API, enabling external systems to subscribe to real-time CRM changes with pull-based flow control and event-level deduplication IDs. Conflict resolution follows a last-write-wins model at the field level for CRM records, and organizations can layer custom logic through automation workflows or middleware to enforce domain-specific merge and precedence rules when reconciling data across systems.

**Review:** SME Review
_Internal note: Verify specific conflict resolution strategies for MDM/synchronization architecture — advanced merge rules may require custom implementation or middleware._

**Sources:**
- https://developer.salesforce.com/docs/data/data-cloud-int/references/data-cloud-ingestionapi-ref/c360-a-real-time-ingestion-api.html
- https://developer.salesforce.com/blogs/2022/10/design-considerations-for-change-data-capture-and-platform-events
- https://www.salesforce.com/data/connectivity/zero-copy/

---

## Product Names Mode Examples

When the user explicitly requests product names, use Salesforce product names directly. These examples show the product-names-on style. **Do not use this style unless the user opts in.**

---

### Q: Does your platform support multi-factor authentication?

**Answer:** Yes. Salesforce enforces multi-factor authentication (MFA) for all direct UI logins and supports MFA for API access.

MFA has been mandatory for all Salesforce products since February 2022. Salesforce supports multiple MFA methods including the Salesforce Authenticator app, third-party TOTP authenticators (Google Authenticator, Microsoft Authenticator), and hardware security keys (U2F/WebAuthn). For SSO environments, MFA can be enforced at the identity provider level. Admins can configure session security levels and step-up authentication for high-assurance operations.

**Review:** Auto-approved
**Sources:**
- https://help.salesforce.com/s/articleView?id=sf.security_overview_2fa.htm

---

### Q: How does your AI/ML offering work and what safeguards exist?

**Answer:** Salesforce provides AI capabilities through Einstein and Agentforce, spanning predictive AI (lead scoring, forecasting), generative AI (Einstein GPT for content generation), and autonomous AI agents (Agentforce).

All AI features operate within the Einstein Trust Layer, which provides: prompt defense (injection detection), data masking of sensitive fields before LLM processing, toxicity detection on outputs, a full audit trail of AI interactions, and data grounding using only the customer's Salesforce data. The Trust Layer ensures no customer data is used to train Salesforce's AI models. Customers can also bring their own models (BYOM) via Einstein Model Builder for custom predictions.

**Review:** Auto-approved
**Sources:**
- https://help.salesforce.com/s/articleView?id=sf.generative_ai_trust_layer.htm
- https://www.salesforce.com/artificial-intelligence/
