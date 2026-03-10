# Single Answer Template

Use this format when responding to individual RFP questions in a freeform Q&A format.

## Standard Format

```
### Q[number]: [Original question text]

**Answer:** [Direct, concise answer in 1-2 sentences]

[Supporting detail: 2-5 sentences expanding on the answer with specifics, certifications, product names, or metrics as appropriate]

**Review:** [Auto-approved | SME Review | Legal Review]
**Sources:**
- [Official doc URL from reference folder]
- [Additional official or blog URL if needed]
```

### Standard Format Example

```
### Q7: Does your platform support multi-factor authentication?

**Answer:** Yes. The platform enforces multi-factor authentication (MFA) for all direct UI logins and supports MFA for API access.

MFA has been mandatory since February 2022. Multiple MFA methods are supported including a native authenticator app, third-party TOTP authenticators (Google Authenticator, Microsoft Authenticator), and hardware security keys (U2F/WebAuthn). For SSO environments, MFA can be enforced at the identity provider level. Admins can configure session security levels and step-up authentication for high-assurance operations.

**Review:** Auto-approved
**Sources:**
- https://help.salesforce.com/s/articleView?id=sf.security_overview_2fa.htm
```

## Concise Format

Use when the user requests brevity. Combine the answer and supporting detail into 2-3 dense sentences. No separate supporting detail block.

```
### Q: [Original question text]

**Answer:** [2-3 dense sentences combining the direct answer and key supporting details. No separate detail block.]

**Review:** [Auto-approved | SME Review | Legal Review]
**Sources:**
- [Official doc URL from reference folder]
- [Additional official or blog URL if needed]
```

### Concise Format Example (Auto-approved)

```
### Q: Can external data be imported into your platform (campaigns, contact lists, provider profiles)?

**Answer:** Yes. The platform supports importing external data through 200+ pre-built connectors (spanning CRMs, marketing tools, databases, cloud storage, and ERP systems), batch and streaming Ingestion APIs for programmatic loads, file-based imports (CSV, Parquet via Amazon S3, Google Cloud Storage, Azure Storage, or SFTP), and zero-copy federation with data warehouses like Snowflake, Databricks, and BigQuery that makes external data queryable without duplication. Once ingested, identity resolution unifies imported records -- such as campaigns, contact lists, and provider profiles -- into a harmonized data model that is immediately usable across segmentation, automation, and AI workflows.

**Review:** Auto-approved
**Sources:**
- https://developer.salesforce.com/docs/data/data-cloud-int/guide/c360-a-thirdparty-connectors.html
- https://www.salesforce.com/data/
```

## Review Flags

The `**Review:**` field is for **internal triage only** — strip it before sending to the customer. See **SKILL.md → Step 5: Assign Review Flags** for the canonical flag definitions (`Auto-approved`, `SME Review`, `Legal Review`) and classification rules.

