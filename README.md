# rfp-answering

Agent skill for answering Salesforce RFPs, RFIs, and vendor questionnaires. Fetches live official Salesforce documentation and drafts responses positioning the Salesforce platform as the vendor solution.

## Quickstart

```
# Claude Code
mkdir -p ~/.claude/skills
git clone https://github.com/sfdc-seadong/rfp-answering ~/.claude/skills/rfp-answering

# Cursor
mkdir -p ~/.cursor/skills
git clone https://github.com/sfdc-seadong/rfp-answering ~/.cursor/skills/rfp-answering
```

Restart your runtime. The skill is active in the next session. Paste RFP questions into chat and it triggers automatically.

## Runtime requirements

Works in any agent runtime with:

- **Skill auto-discovery** from a skills directory (`~/.claude/skills/` for Claude Code, `~/.cursor/skills/` for Cursor).
- **Subagent / task dispatch** — the orchestrator spawns subagents per topic cluster.
- **Web fetch and search** — subagents pull live Salesforce documentation.

Tool names differ per runtime (`Task` / `WebFetch` / `WebSearch` in Claude Code; equivalents in Cursor). The skill instructions translate across runtimes.

Does NOT work on Claude.ai (web) — no skill discovery, no subagents.

## Usage modes

**Without Google Workspace MCP (default):**
Paste RFP questions into chat. The skill drafts answers with sources. You copy results into your RFP document manually.

**With Google Workspace MCP (optional):**
Point the skill at a Google Sheet URL. It reads questions, detects column structure, drafts answers, and writes them back into the correct cells. See install steps below.

## Optional: Google Workspace MCP

For direct read/write to Google Sheets and Docs. Two options — `google-adc` is recommended.

### Option A: `google-adc` (recommended)

Authenticates via Application Default Credentials (reuses gcloud's built-in OAuth client), so it works inside Workspace orgs that restrict third-party OAuth apps.

Prereqs:

- `gcloud` CLI — https://cloud.google.com/sdk/docs/install
- `uv` — https://docs.astral.sh/uv/getting-started/installation/

Install:

```
git clone https://github.com/smian1/google-adc-mcp.git ~/google-mcp
cd ~/google-mcp
./setup-google-adc.sh
```

The setup script runs `gcloud auth application-default login`, pins a quota project, and configures scopes.

Register the MCP server with your runtime:

- **Claude Code** — add to `~/.claude.json` under `mcpServers`:
  ```json
  "google-adc": {
    "command": "uv",
    "args": ["run", "--script", "/Users/<you>/google-mcp/server.py"],
    "env": {
      "GOOGLE_ADC_QUOTA_PROJECT": "<your-gcp-quota-project>"
    }
  }
  ```
- **Cursor** — add the same entry to your Cursor MCP config (Settings → MCP → Edit Config).

Restart your runtime. The `mcp__google-adc__*` tools appear in the tool list.

Gotcha: re-running `gcloud auth application-default login` wipes the quota project. If auth stops working, re-run `./setup-google-adc.sh`.

### Option B: `mcp-gsheets` (fallback)

Sheets-only. Requires a Google Cloud service account and JSON key. See https://github.com/xing5/mcp-google-sheets for setup.

## What's included

- `SKILL.md` — the skill definition (orchestrator workflow, scoring strategy, accuracy guardrails, tone rules)
- `reference/` — topic-specific reference files (platform, security, Data 360, integrations, etc.)
- `templates/` — answer templates and the subagent prompt template
- `examples/` — sample Q&A for tone calibration
- `docs/` — skill consistency audit and internal notes

## What's not included

`scripts/` (deal-specific runtime scripts with customer names and sheet IDs) is gitignored. The skill runs fine without them.

## Troubleshooting

**Skill doesn't trigger.** Confirm the clone landed in the right place: `ls ~/.claude/skills/rfp-answering/SKILL.md` (or `~/.cursor/skills/...`). Restart the runtime after cloning.

**Sheet URLs don't work.** The Google Workspace MCP isn't installed or registered. Use "paste questions" mode instead, or install `google-adc`.

**Orchestrator says it needs user approval before spawning subagents.** That's by design — the skill shows a summary table first. Respond "proceed" or adjust the plan.

**Subagent answers have wrong tone/depth.** The skill's Tone & Style section is authoritative. If existing answers in a sheet are influencing output, explicitly tell the orchestrator "do not adapt tone from existing answers."
