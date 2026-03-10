# Security & Compliance - Reference

> **Last reviewed:** 2026-03

Reference material for Salesforce certifications, encryption, authentication, vulnerability management, and security practices.

## Certifications & Attestations

### Stable URLs
- https://compliance.salesforce.com/en
- https://trust.salesforce.com/en/compliance/

## Security Overview & Practices

### Stable URLs
- https://security.salesforce.com/
- https://trust.salesforce.com/en/security/

### Search Queries
- "security overview site:help.salesforce.com"

## Encryption

### Stable URLs
- https://developer.salesforce.com/docs/atlas.en-us.securityImplGuide.meta/securityImplGuide/security_pe_concepts.htm

### Search Queries
- "Shield Platform Encryption overview site:help.salesforce.com"
- "encryption at rest site:help.salesforce.com"

## Multi-Factor Authentication (MFA)

### Search Queries
- "MFA multi-factor authentication overview site:help.salesforce.com"

## Single Sign-On (SSO)

### Search Queries
- "SSO single sign-on SAML overview site:help.salesforce.com"
- "identity provider service provider site:help.salesforce.com"

## Salesforce Shield

### Stable URLs
- https://www.salesforce.com/platform/shield/

### Search Queries
- "event monitoring site:help.salesforce.com"
- "field audit trail site:help.salesforce.com"

## Vulnerability & Penetration Testing

### Stable URLs
- https://trust.salesforce.com/en/security/penetration-testing/

### Search Queries
- "security health check site:help.salesforce.com"

## Incident Response & Trust

### Stable URLs
- https://trust.salesforce.com/en/
- https://trust.salesforce.com/en/trust-and-compliance-documentation/

## FedRAMP / Government Cloud

### Stable URLs
- https://www.salesforce.com/solutions/industries/government/
- https://trust.salesforce.com/en/compliance/

## HIPAA

### Search Queries
- "HIPAA eligibility site:help.salesforce.com"

## Security Best Practices (Developer)

### Stable URLs
- https://developer.salesforce.com/docs/atlas.en-us.securityImplGuide.meta/securityImplGuide/
- https://architect.salesforce.com/decision-guides/security

## Key Native Capabilities

When reference URLs fail or return thin results, use this section as a fallback. These capabilities are natively available and should not be described as requiring custom build or external tools.

| Capability | Native? | Notes |
|---|---|---|
| AES-256 encryption at rest | Yes | Platform-managed; applies to all data at the infrastructure layer. Shield Platform Encryption (add-on) adds field-level BYOK encryption. |
| TLS 1.2+ encryption in transit | Yes | Perfect Forward Secrecy enabled |
| MFA enforcement | Yes | Mandatory for all direct UI logins since Feb 2022 |
| SAML 2.0 / OpenID Connect SSO | Yes | IdP and SP modes |
| SCIM 2.0 user provisioning | Yes | Automated lifecycle management |
| OAuth 2.0 API authentication | Yes | Multiple grant types supported |
| Field-level security | Yes | Per-profile and per-permission-set |
| IP range restrictions | Yes | Login and API access controls |
| Session security settings | Yes | Timeout, step-up authentication |
| Health Check security assessment | Yes | Built-in security scoring dashboard |
| Shield Platform Encryption (BYOK) | Yes (add-on) | Field-level encryption with customer-managed keys |
| Shield Event Monitoring | Yes (add-on) | Login, API, and data access audit logs |
| Shield Field Audit Trail | Yes (add-on) | 10-year field history retention |
| SOC 1/2/3, ISO 27001/27017/27018 | Yes | Third-party attested |
| FedRAMP Moderate and High | Yes | Government Cloud only |
| HIPAA eligibility | Yes | Requires BAA and Shield |
| PCI DSS Level 1 | Yes | For Commerce Cloud |

## Search Fallback

If none of the above cover a specific security question, search:
`"[topic] site:trust.salesforce.com"` or `"[topic] site:security.salesforce.com"` or `"[topic] security site:help.salesforce.com"`
