# rfp-answering

Claude Code skill for answering Salesforce RFPs, RFIs, and vendor questionnaires. Fetches live official Salesforce documentation and drafts responses positioning the Salesforce platform as the vendor solution.

## Install

Clone into your Claude Code skills directory:

```
git clone https://github.com/sfdc-seadong/rfp-answering ~/.claude/skills/rfp-answering
```

Claude Code auto-discovers skills under `~/.claude/skills/`. The skill is active in your next session.

## Prerequisites

Drafting works out of the box. Reading from / writing to Google Sheets and Docs requires Google MCP servers:

- `mcp__google-adc__*` — Google Workspace tools (Sheets, Docs, Drive, Gmail, Calendar). Preferred.
- `mcp__mcp-gsheets__*` — fallback Sheets-only tools.

Without these, the skill still drafts answers; you copy them into the sheet manually.

### Install `google-adc` MCP

This is the recommended MCP server for Google Workspace access. It authenticates via Application Default Credentials (reusing gcloud's built-in OAuth client), so it works inside Workspace orgs that restrict third-party OAuth apps.

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

Register with Claude Code — add to `~/.claude.json` under `mcpServers`:

```json
"google-adc": {
  "command": "uv",
  "args": ["run", "--script", "/Users/<you>/google-mcp/server.py"],
  "env": {
    "GOOGLE_ADC_QUOTA_PROJECT": "<your-gcp-quota-project>"
  }
}
```

Restart Claude Code. The `mcp__google-adc__*` tools appear in the tool list.

Gotcha: re-running `gcloud auth application-default login` wipes the quota project. If auth stops working, re-run `./setup-google-adc.sh`.

## Usage

Trigger the skill by mentioning RFP, RFI, vendor questionnaire, or proposal response in your prompt. Examples:

- "Help me answer this RFP: [paste questions]"
- "Fill in the missing answers on this Google Sheet: [URL]"
- "Draft RFI responses for these security questions"

The orchestrator parses, classifies by category, spawns subagents per topic cluster, and returns drafted answers with sources.

## What's included

- `SKILL.md` — the skill definition (orchestrator workflow, scoring strategy, accuracy guardrails, tone rules)
- `reference/` — topic-specific reference files (platform, security, Data 360, integrations, etc.)
- `templates/` — answer templates and subagent prompt template
- `examples/` — sample Q&A for tone calibration

## What's not included

`scripts/` (deal-specific runtime scripts) is gitignored. The skill runs fine without them.
