# Spreadsheet / Tabular RFP Template

Use this format when the RFP requires responses in a table or spreadsheet format.

## Format

```markdown
| # | Question | Answer | Compliance | Notes |
|---|----------|--------|------------|-------|
| 1 | [Question text] | [Answer — length per format-defaults] | [Yes / Partial / No / N/A] | [Caveats, add-on required, or verification needed] |
```

## Column Definitions

- **#**: Question number from the original RFP
- **Question**: Original question text (verbatim or summarized)
- **Answer**: See [format-defaults.md](../reference/format-defaults.md) for length. Lead with the direct answer. **Inline mode (no dedicated URL column):** Answer must end with a `Sources:` block — sources are part of the cell text so they survive copy/paste and sheet writes. **Separate column mode (sheet has a dedicated URL column):** Omit Sources from the Answer cell; put URLs in the designated column.
- **Compliance**: Assessment of whether the capability is available without additional licensing
  - **Yes** -- Fully supported out of the box or with standard configuration
  - **Partial** -- Supported with add-on licensing, custom development, or specific edition
  - **No** -- Not supported
  - **N/A** -- Not applicable to Salesforce's delivery model
  - Note: Compliance reflects licensing/availability, not capability depth. An answer can be `Partial` (requires add-on) and still score at the highest rubric level if the capability fully meets the requirement once licensed.
- **Notes**: Any caveats, such as:
  - "Requires add-on encryption license"
  - "Available in Enterprise Edition and above"
  - "Requires Hyperforce provisioning; region availability varies by contract"
  - "Requires customer-side configuration"

## Internal Review Flags

Every answer gets a review flag for internal triage. These flags are **never included in customer-facing responses** — they go in a separate "Review" column (or a dedicated "Review" tab when writing to Google Sheets).

See **SKILL.md → Step 5: Assign Review Flags** for the canonical flag definitions (`Auto-approved`, `SME Review`, `Legal Review`) and classification rules.

## Example

```markdown
| # | Question | Answer | Compliance | Notes | Review |
|---|----------|--------|------------|-------|--------|
| 1 | Do you encrypt data at rest? | Yes. All data at rest is encrypted using AES-256. Add-on field-level encryption with customer-managed keys (BYOK) is available.\n\nSources:\nhttps://help.salesforce.com/s/articleView?id=sf.security_pe_overview.htm\nhttps://help.salesforce.com/s/articleView?id=sf.security_encryption_at_rest.htm | Yes | Add-on encryption license required for BYOK and field-level encryption. | Auto-approved |
| 2 | Do you support SAML-based SSO? | Yes. The platform supports SAML 2.0 as both an Identity Provider and Service Provider.\n\nSources:\nhttps://help.salesforce.com/s/articleView?id=sf.sso_about.htm | Yes | | Auto-approved |
| 3 | Can data be stored exclusively in the EU? | Yes. The platform's public cloud infrastructure enables deployment in EU regions (Germany, France, UK).\n\nSources:\nhttps://help.salesforce.com/s/articleView?id=sf.data_residency.htm | Yes | Requires Hyperforce provisioning; region availability varies by contract. | Legal Review |
| 4 | Do you provide source code escrow? | Source code escrow is not applicable. As a SaaS platform, the service is continuously delivered and maintained by the vendor.\n\nSources:\nhttps://www.salesforce.com/company/legal/agreements/ | N/A | SaaS delivery model; escrow is not applicable. | Auto-approved |
```

> **Note on cell formatting:** The `\n` above represents newlines inside a single cell. In Google Sheets, the answer text and `Sources:` block are written as one multi-line string in the Answer cell.

## Google Sheets Review Tab

When writing answers to a Google Sheet, write review flags using one of these approaches (in order of preference):

1. **Separate "Review" tab** — Create a new sheet tab called "Review" with columns: `#`, `Sheet`, `Review Flag`, `Review Notes`, `Answered At`. The `Sheet` column tracks which tab the question came from (e.g., "Functional Reqs", "Technical Reqs") to avoid ambiguity when multiple tabs share row numbers. `Answered At` records the timestamp in US Central Time using the format `MM/DD/YYYY h:mm AM/PM CT` (e.g., `03/07/2026 1:54 PM CT`) when the answer was written. This keeps internal flags invisible to anyone who only sees the main response sheet.
2. **Hidden column** — Add the Review column to the main sheet and hide it after writing. Less preferred because it's easy to accidentally unhide before submission.

## Guidelines

- Match the original RFP's numbering exactly.
- If the original RFP uses different column headers, adapt this template to match.
- Always assign a review flag to every answer — the review team uses these to triage their limited review time.
- Sources: See [format-defaults.md](../reference/format-defaults.md). Use newline-separated URLs in sheet cells (no bullets).

### Answer Depth

Answer length: see [format-defaults.md](../reference/format-defaults.md).

**When the template has separate Answer + Notes/Detail columns:**
- Write the full answer in the Answer column (length per format-defaults). Lead with the direct answer in the first sentence.
- Use the Notes column for compliance caveats, add-on requirements, or verification notes — not for splitting the narrative.

**When the template has a single response column:**
- Write a self-contained response (length per format-defaults). Shorter questions get shorter answers — do not pad.
- Lead with the direct answer in the first sentence. Follow with specific mechanisms, capabilities, and how the platform meets the requirement.
- Include caveats, limitations, or configuration details inline rather than omitting them.

**How to detect which mode to use:**
- Read the customer's column headers before writing. If there is only one response column (e.g., "Vendor Response", "Supporting Evidence", "Comments"), use the single-column format.
- If the template has multiple response columns (e.g., "Answer" + "Notes" + "Compliance"), put the full answer in the Answer column; Notes is for supplementary caveats only.
- When in doubt, default to a thorough answer per format-defaults.
