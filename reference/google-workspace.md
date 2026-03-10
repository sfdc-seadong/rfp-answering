# Google Workspace Integration

The RFP skill supports reading from and writing to Google Sheets and Google Docs. When the user shares a Google URL, detect the document type and use the appropriate approach.

## Service Account & Access

A Google service account is configured at `/Users/sea.dong/mcp-servers/mcp-gsheets/` with credentials at `service-account-key.json`.

**Service account email:** `rfp-sheets-agent@ehc-sea-dong-c4f13a.iam.gserviceaccount.com`

When accessing a Google document for the first time:

1. Attempt to read the document using the Google API (via the `googleapis` npm package in the mcp-gsheets directory).
2. If access fails with a **403 Permission Denied** error, immediately instruct the user to share the document with the service account email above (Editor access for Sheets the agent will write to, Viewer for read-only Docs).
3. Once the user confirms sharing, retry the API call.

## Connecting to Google APIs

The `mcp-gsheets` MCP server may or may not be registered in Cursor's runtime. Use this fallback order:

1. **Try `CallMcpTool`** with server `user-mcp-gsheets` first. Note: Cursor prefixes user-defined MCP servers with `user-`; the server is defined as `mcp-gsheets` in `~/.cursor/mcp.json` but registered as `user-mcp-gsheets` at runtime. Available tools:

   | Tool | Use For |
   |------|---------|
   | `sheets_check_access` | Verify permissions before reading/writing |
   | `sheets_get_metadata` | List all tabs, discover sheet structure |
   | `sheets_get_values` | Read a single range (e.g., one tab's headers) |
   | `sheets_batch_get_values` | Read multiple ranges in one call — use this to read headers from all tabs at once |
   | `sheets_update_values` | Write to a single range |
   | `sheets_batch_update_values` | Write to multiple ranges in one call — primary tool for writing answers |
   | `sheets_insert_sheet` | Create a new tab — use this to create the Review tab |
   | `sheets_append_values` | Append rows to an existing table — use this to add entries to an existing Review tab (set `insertDataOption: "INSERT_ROWS"` to avoid overwriting) |
2. **If the MCP server is unavailable**, call the Google API directly by writing and running a `.cjs` script in `/Users/sea.dong/mcp-servers/mcp-gsheets/` (the `googleapis` package and service account key are already installed there). Clean up the script after use.

## URL Detection

| URL Pattern | Document Type | API |
|-------------|--------------|-----|
| `docs.google.com/spreadsheets/d/{id}` | Google Sheet | Google Sheets API v4 |
| `docs.google.com/document/d/{id}` | Google Doc | Google Docs API v1 |

Extract the document ID from between `/d/` and the next `/`.

## Reading RFP Questions from a Sheet

### Step 1: Discover Tabs

1. Extract the spreadsheet ID from the URL.
2. Call `sheets_get_metadata` to list all tabs by name.
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

Use `sheets_batch_get_values` to read the header row (typically row 1) from every question tab in a single call. This reveals each tab's column structure — which columns hold question numbers, question text, response fields, scoring, notes, and documentation URLs.

Different tabs in the same RFP often use different column layouts. Record the column mapping per tab.

### Step 4: Read All Questions

Read the question content from each tab. For large tabs (100+ rows), read in chunks to avoid API payload limits.

**Separator row detection:** RFP sheets often intersperse section headers and blank rows between questions. A row is a separator (not a question) if:
- It has no value in the question-number column, OR
- Fewer than 2 cells in the row are populated, OR
- The row contains a single text value spanning what appears to be a section label (e.g., "SECURITY REQUIREMENTS")

Skip separator rows when counting questions, but preserve their row numbers for accurate write-back mapping.

### Step 5: Track Tab-to-Question Mapping

For each question, record:
- Original question number (as shown in the sheet)
- Sheet row number (for write-back)
- Tab name (for write-back to the correct tab)
- Tab-specific column mapping (which column to write the answer in, the score, the URL, etc.)

This mapping is essential for multi-tab write-back — the orchestrator needs to know that question #42 lives in row 47 of the "NFR" tab, with the answer going in column E.

## Writing Answers Back to a Sheet

1. **Standard mode (1-9 questions):** Present the proposed scores, evidence text, and target cell references to the user for approval before writing — Standard mode has no earlier approval checkpoint. **Batch and Parallel Agent modes:** Write directly — the user already approved the plan (Phase 1) and calibrated tone (Phase 2/3), so a third approval gate is unnecessary.
2. Use the tab-to-question mapping from the read phase to write each answer to the correct tab, row, and column. Different tabs may use different column structures.
3. If the RFP sheet has specific columns for answers (e.g., "Vendor Response", "Compliance Status", "Notes"), map the template fields to those columns.
4. Use `sheets_batch_update_values` to write all answers. For large answer sets (50+ questions), split into chunks of 25-40 rows per call.
5. **Review tab:**
   - Check if a "Review" tab already exists (from `sheets_get_metadata`).
   - If it does not exist, create it with `sheets_insert_sheet` (title: "Review").
   - If it already has entries from a prior session, use `sheets_append_values` with `insertDataOption: "INSERT_ROWS"` to add new review entries after the existing ones.
   - If it is empty or newly created, write headers and entries with `sheets_batch_update_values`.
   - See [spreadsheet-format.md](../templates/spreadsheet-format.md) for the column spec and timestamp format.

## Reading RFP Questions from a Google Doc

1. Extract the document ID from the URL.
2. Use the Google Docs API to read the document body content.
3. Parse questions from the document structure (headings, numbered lists, tables).
4. Proceed with the normal workflow (Steps 2-5 in SKILL.md). Write answers back to a Sheet if one is provided, or present them in chat.
