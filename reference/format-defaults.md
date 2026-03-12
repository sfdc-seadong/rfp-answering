# Format Defaults

Canonical definitions for RFP answer formatting. **This is the single source of truth** — update this file to change values used across all templates.

## Answer Length

- **Default:** 4-12 sentences across 2-3 paragraphs
- **Applies to:** Single-answer format, spreadsheet format (all column structures)
- **Guidance:** Simpler questions get shorter answers; do not pad to fill 12 sentences when 4 suffice. Lead with the direct answer in sentence one.
- **Concise mode override:** When the user requests brevity, use 2-3 dense sentences instead.

## Sources

- **Count:** 1-3 URLs per answer. Cite every claim; prefer the strongest 1-3 official sources.
- **Order:** Official doc URLs first (help.salesforce.com, developer.salesforce.com, architect, trust, trailhead), blog links second.
- **Placement:** Inline by default — end each answer with a `Sources:` block. Omit when the sheet has a dedicated documentation/URL column (see SKILL.md Document Format Detection, or format directives in TONE_CALIBRATION).
- **Format:**
  - Chat / markdown: `**Sources:**` followed by bullet list (`- https://...`)
  - Spreadsheet cell: `Sources:` on its own line, then one URL per line (no bullets; newlines render in cells)
