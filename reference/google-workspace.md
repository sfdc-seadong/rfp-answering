# Google Workspace Integration

The RFP skill supports reading from and writing to Google Sheets and Google Docs. When the user shares a Google URL, detect the document type and use the appropriate approach.

## Access Model (Claude Code)

Two Google integrations are registered. **Prefer `mcp__google-adc__*` first** — it uses the user's own Google OAuth (Application Default Credentials), so it can reach any Sheet, Doc, Drive file, Gmail, Calendar, etc. that the user already has access to. **No sharing step is required.**

| Preference | MCP prefix | Auth | Reach |
|------------|-----------|------|-------|
| **1st (default)** | `mcp__google-adc__*` | User's Google OAuth (ADC) | Anything the user can access |
| 2nd (fallback) | `mcp__mcp-gsheets__*` | Service account | Only docs shared with `rfp-sheets-agent@ehc-sea-dong-c4f13a.iam.gserviceaccount.com` |
| 3rd (last resort) | Direct `googleapis` script in `/Users/sea.dong/mcp-servers/mcp-gsheets/` | Service account key | Same as #2 |

**Do NOT prompt the user to share a sheet with the service account on the first attempt.** Try `mcp__google-adc__*` first. Only fall back to the service account MCP if an ADC call returns "tool not available" or a non-403 error that the service-account path can work around. If the ADC call returns 403/404 for a sheet the user says they own, the issue is likely the URL or OAuth scope — re-verify before falling back.

## Connecting to Google APIs

### Path 1 (preferred): `mcp__google-adc__*` — user OAuth

Use these tools for Sheets operations:

| Tool | Use For |
|------|---------|
| `mcp__google-adc__sheets_get_info` | List all tabs, discover sheet structure (equivalent to `sheets_get_metadata`) |
| `mcp__google-adc__sheets_read` | Read a range |
| `mcp__google-adc__sheets_write` | Write to a range |
| `mcp__google-adc__sheets_add_tab` | Create a new tab (use for Review tab) |
| `mcp__google-adc__sheets_format_cells` | Cell formatting |
| `mcp__google-adc__sheets_create` | Create a new spreadsheet |

Also available under `mcp__google-adc__*`: Gmail (`gmail_search`, `gmail_get_message`, ...), Drive (`drive_search`, `drive_get_content`, ...), Docs (`docs_get_text`, `docs_create`, ...), Calendar, Forms, Slides, Tasks.

### Path 2 (fallback): `mcp__mcp-gsheets__*` — service account

Only use when Path 1 is unavailable. The service account (`rfp-sheets-agent@ehc-sea-dong-c4f13a.iam.gserviceaccount.com`) requires the user to explicitly share the sheet first (Editor for write, Viewer for read). Available tools:

   | Tool | Use For |
   |------|---------|
   | `mcp__mcp-gsheets__sheets_check_access` | Verify permissions before reading/writing |
   | `mcp__mcp-gsheets__sheets_get_metadata` | List all tabs, discover sheet structure |
   | `mcp__mcp-gsheets__sheets_get_values` | Read a single range |
   | `mcp__mcp-gsheets__sheets_batch_get_values` | Read multiple ranges in one call |
   | `mcp__mcp-gsheets__sheets_update_values` | Write to a single range |
   | `mcp__mcp-gsheets__sheets_batch_update_values` | Batch-write multiple ranges |
   | `mcp__mcp-gsheets__sheets_insert_sheet` | Create a new tab (use for Review tab) |
   | `mcp__mcp-gsheets__sheets_append_values` | Append rows (set `insertDataOption: "INSERT_ROWS"` to avoid overwriting) |

If accessing for the first time via Path 2 and it fails with **403 Permission Denied**, instruct the user to share the document with the service account email, then retry.

### Path 3 (last resort): direct `googleapis` script

If both MCPs are unavailable, write and run a `.cjs` script in `/Users/sea.dong/mcp-servers/mcp-gsheets/` (the `googleapis` package and service account key are already installed there). Clean up the script after use. This path also uses the service account, so sharing is required.

## URL Detection

| URL Pattern | Document Type | API |
|-------------|--------------|-----|
| `docs.google.com/spreadsheets/d/{id}` | Google Sheet | Google Sheets API v4 |
| `docs.google.com/document/d/{id}` | Google Doc | Google Docs API v1 |

Extract the document ID from between `/d/` and the next `/`.

## Reading RFP Questions from a Sheet

### Step 1: Discover Tabs

1. Extract the spreadsheet ID from the URL.
2. Call `mcp__google-adc__sheets_get_info` (preferred) or `mcp__mcp-gsheets__sheets_get_metadata` (fallback) to list all tabs by name.
3. Classify each tab by its likely role:

   | Tab Name Patterns | Role | Action |
   |-------------------|------|--------|
   | "Instructions", "How to Respond", "Scoring Guide", "Rubric", "Cover Page", "Overview" | Instructions / rubric | Read for scoring rubric definitions and response guidelines. Do NOT write answers here. |
   | "Review" | Review flags | Reserved for internal review flags. Read existing entries to determine append offset. |
   | Most other names (e.g., "Functional Requirements", "NFR", "Security", "Commercial Proposal", "Data Management") | Question tabs | Read headers and questions. These are where answers get written. |

   When in doubt about a tab's role, read its first 5 rows — question tabs have columnar headers with fields like "Requirement", "Question", "Response", "Score", etc.

### Step 2: Detect Scoring Rubric

Before classifying questions, check instruction-type tabs for custom scoring rubric definitions. Many complex RFPs define their scoring scale (e.g., 1/3/5 with specific descriptions per level) on a separate tab rather than in column headers. If found, pass the rubric definition to all subagents via `{{TONE_CALIBRATION}}`.

### Step 3: Read Headers from All Question Tabs

Read the header row (typically row 1) from every question tab. Use `mcp__google-adc__sheets_read` (preferred — one call per tab) or `mcp__mcp-gsheets__sheets_batch_get_values` (fallback — reads multiple ranges in one call). This reveals each tab's column structure — which columns hold question numbers, question text, response fields, scoring, notes, and documentation URLs.

Different tabs in the same RFP often use different column layouts. Record the column mapping per tab.

### Step 4: Read All Questions and Build Question-to-Row Mapping

Read the question content from each tab. For large tabs (100+ rows), read in chunks to avoid API payload limits.

**Separator row detection:** RFP sheets often intersperse section headers and blank rows between questions. A row is a separator (not a question) if:
- It has no value in the question-number column, OR
- Fewer than 2 cells in the row are populated, OR
- The row contains a single text value spanning what appears to be a section label (e.g., "SECURITY REQUIREMENTS")

Skip separator rows when counting questions, but preserve their row numbers for accurate write-back mapping.

**MANDATORY: Build question-to-row mapping from the sheet.** Do not assume row N = question N. Section headers and blank rows create gaps — e.g., Q28 at row 30, header at row 29, Q29 at row 31. For sheets with multiple question tabs, iterate each question tab (in tab order) and include the tab name in each mapping entry so write-back targets the correct tab and row. Iterate over sheet rows (chunked for large sheets) and record, in order, each row where the question column identified in Step 3 (the column holding question text, often labeled "Question", "Requirement", or similar) has a non-empty value. This produces a mapping: question_index 1 → row X, question_index 2 → row Y, etc. Persist this mapping (e.g., `sheet-question-rows.json`) before drafting or spawning agents. Use it when writing answers so each answer lands in the correct cell beside its question.

### Step 5: Track Tab-to-Question Mapping

For each question, record:
- Original question number (as shown in the sheet)
- Sheet row number (for write-back)
- Tab name (for write-back to the correct tab)
- Tab-specific column mapping (which column to write the answer in, the score, the URL, etc.)

This mapping is essential for multi-tab write-back — the orchestrator needs to know that question #42 lives in row 47 of the "NFR" tab, with the answer going in column E.

## Writing Answers Back to a Sheet

1. **Approval flow:** The user approves the plan in Phase 1 (summary table) before drafting. Write directly after subagents complete — no additional approval gate.
2. Use the question-to-row mapping built during format detection (from reading the sheet row-by-row) to write each answer to the correct tab, row, and column. **Never assume sequential row numbers** — section headers and blank rows mean question N may not be in row N. Different tabs may use different column structures.
3. If the RFP sheet has specific columns for answers (e.g., "Vendor Response", "Compliance Status", "Notes"), map the template fields to those columns.
4. Write all answers. Preferred: one `mcp__google-adc__sheets_write` call per range. Fallback: `mcp__mcp-gsheets__sheets_batch_update_values` (one call covers multiple ranges). For large answer sets (50+ questions), split into chunks of 25-40 rows per call.
5. **Review tab:**
   - Check if a "Review" tab already exists (from the tab discovery call in Step 1).
   - If it does not exist, create it with `mcp__google-adc__sheets_add_tab` (preferred) or `mcp__mcp-gsheets__sheets_insert_sheet` (fallback). Title: "Review".
   - If it already has entries from a prior session, append new entries after the existing ones. Preferred: `mcp__google-adc__sheets_write` to a range starting below the last row. Fallback: `mcp__mcp-gsheets__sheets_append_values` with `insertDataOption: "INSERT_ROWS"`.
   - If it is empty or newly created, write headers and entries with `mcp__google-adc__sheets_write` (preferred) or `mcp__mcp-gsheets__sheets_batch_update_values` (fallback).
   - See [spreadsheet-format.md](../templates/spreadsheet-format.md) for the column spec and timestamp format.

## Reading RFP Questions from a Google Doc

1. Extract the document ID from the URL.
2. Use the Google Docs API to read the document body content.
3. Parse questions from the document structure (headings, numbered lists, tables).
4. Proceed with the normal workflow (Steps 2-5 in SKILL.md). Write answers back to a Sheet if one is provided, or present them in chat.
