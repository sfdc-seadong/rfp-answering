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

- `mcp__google-adc__*` — Google Workspace tools (Sheets, Docs, Drive). Preferred.
- `mcp__mcp-gsheets__*` — fallback Sheets tools.

Install one or both before running on a Google-hosted RFP. Without them, the skill still drafts answers; you copy them into the sheet manually.

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
