# RFP Skill Consistency Audit

Review of all skill files for inconsistencies, conflicting instructions, and gaps. Date: 2026-03-12.

**Updates (2026-03-12):** Items 1–7 and 9 from the summary below have been addressed. Items 6 (Persona), 8 (Step 3 order), and 10 (hardcoded numbers) were left as low-priority optional changes.

---

## 1. Pasted/Chat-Only Flow — No Sheet Guidance

**Location:** [SKILL.md](../SKILL.md) Step 3, Document Format Detection, [reference/google-workspace.md](../reference/google-workspace.md)

**Issue:** The workflow assumes a Google Sheet. Step 3 says "Detect document format **from the sheet**" and Document Format Detection says "detect these FORMAT signals **from the sheet**." When the user pastes questions in chat or provides a Google Doc without a sheet, there is no sheet to read.

**Gap:** No explicit guidance for pasted-text or Doc-only flows. The skill should state: when there is no sheet, use default format (single-answer template, inline Sources, per format-defaults) and proceed with the workflow.

---

## 2. single-answer.md — "Product Names" in Format Placeholder

**Location:** [templates/single-answer.md](../templates/single-answer.md) line 16

**Issue:** The format placeholder says "Supporting paragraph with specifics, certifications, **product names**, or metrics." The default rule is NO Salesforce product names in customer-facing text. Including "product names" in the placeholder could be read as "include product names."

**Recommendation:** Change to "product capabilities" or "named features" to avoid implying product names should be used.

---

## 3. spreadsheet-format.md — Sources Block Rule vs. Separate Column Mode

**Location:** [templates/spreadsheet-format.md](../templates/spreadsheet-format.md) line 17

**Issue:** The Answer column definition says "**Must end with a `Sources:` block**" but format-defaults and SKILL say to omit inline Sources when the sheet has a dedicated URL column. The template does not distinguish inline vs. separate-column mode.

**Recommendation:** Clarify: "When URL placement is inline, the Answer must end with a `Sources:` block. When the sheet has a dedicated URL column, omit Sources from the Answer cell and put URLs in the designated column."

---

## 4. Architecture Diagram — Agent Count Range

**Location:** [SKILL.md](../SKILL.md) architecture diagram, line 287

**Issue:** The diagram says "N = 2–10, driven by question distribution" but the Agent Count table says 1–9 questions → 1 agent. So N can be 1 for small RFPs.

**Recommendation:** Change to "N = 1–10" or "N = 1–10+, driven by question distribution."

---

## 5. Dynamic Agent Sizing — Merge Rule for Small RFPs

**Location:** [SKILL.md](../SKILL.md) Dynamic Agent Sizing, Step 2, lines 411–422

**Issue:** The merge rule says "Merge any category with fewer than 3 questions into the nearest related category" and "After merging, each group should have at least 3 questions." The affinity table only covers Data & Privacy, Support, Integrations, and Competitive Positioning. For 3 questions in 3 different categories (e.g., 1 Security, 1 Data 360, 1 Platform), there is no explicit merge path—Data 360 and Platform are not in the "Merges into" column. The sizing example says "3 Qs → 1 agent" but the rules do not spell out how to get there.

**Recommendation:** Add an explicit rule: "For RFPs with fewer than 3 questions total, merge all into a single agent."

---

## 6. Persona — "Every Answer You Write"

**Location:** [SKILL.md](../SKILL.md) Persona, line 10

**Issue:** Persona says "Every answer **you write** positions the Salesforce platform..." The orchestrator does not write answers; subagents do. The "you" (orchestrator) coordinates but does not draft.

**Recommendation:** Optional clarity: "Every answer produced by this skill" or "Every answer drafted positions..." — or leave as-is if "you" is understood as the skill as a whole.

---

## 7. Subagent-Prompt — "Existing Answers in the Sheet"

**Location:** [templates/subagent-prompt.md](../templates/subagent-prompt.md) line 174

**Issue:** "Do NOT infer tone from any existing answers in the sheet — those are for format detection only." Subagents do not have sheet access, so they would not see existing answers. The text may be legacy from when the main agent drafted.

**Recommendation:** Rephrase to: "Do NOT infer tone from any sample answers the orchestrator may have passed — the skill's guidelines are the authoritative standard." Or remove if redundant.

---

## 8. Step 3 vs. Workflow Phase Order

**Location:** [SKILL.md](../SKILL.md) Step 3 vs. The Workflow Phases 1–2

**Issue:** Step 3 lists "Detect document format" as item 1, then grouping, agent count, present table. The Workflow has Phase 1 (parse, classify, group, present, approve) and Phase 2 (format detection). So format detection is in Phase 2, after grouping. Step 3 can be read as "format first, then group," which does not match the phase order. Functionally fine—format is done before spawning—but the ordering differs.

**Recommendation:** Align Step 3 with the phases: group first (Phase 1), then format detect (Phase 2), or state that Step 3 lists all pre-spawn tasks without strict order.

---

## 9. sample-qa.md — Orphaned Reference

**Location:** [examples/sample-qa.md](../examples/sample-qa.md)

**Issue:** sample-qa.md is not referenced in SKILL.md. The old Step 4 (Draft Answers) used to say "See sample-qa.md for tone and style calibration." After refactoring to Step 4 = Spawn Subagents, that reference was dropped. Phase 2 has an optional "draft 2–3 sample answers" step; the orchestrator could use sample-qa when doing that, but SKILL does not point to it.

**Recommendation:** Add a reference to sample-qa in Phase 2 or in the Tone & Style section as supplemental examples.

---

## 10. Quick Reference / Pre-Flight — Hardcoded Numbers

**Location:** [SKILL.md](../SKILL.md) Quick Reference (lines 37–38), Pre-Flight Checklist (lines 59–60)

**Issue:** Quick Reference and Pre-Flight repeat "4-12 sentences" and "1-3 URLs" even though format-defaults is the source of truth. Templates were updated to defer to format-defaults, but SKILL still inlines the numbers. Low risk of drift, but not strictly single-source.

**Recommendation:** Optional—shorten to "See format-defaults" without repeating numbers, for consistency with templates.

---

## 11. Subagent Return Format — Sources Style

**Location:** [templates/subagent-prompt.md](../templates/subagent-prompt.md) lines 198–202

**Issue:** The Return Format example shows plain "Sources:" followed by URLs, while format-defaults says chat should use "**Sources:**" (bold) and a bullet list. Subagents may return plain text; the orchestrator could format for chat output. If so, this is intentional and OK.

**Status:** Likely intentional—no change needed unless subagents are expected to emit the final chat format.

---

## Summary

| # | Severity | Issue | File(s) |
|---|----------|-------|---------|
| 1 | Medium | No guidance for pasted/chat-only flows (no sheet) | SKILL.md |
| 2 | Low | "Product names" in single-answer placeholder | single-answer.md |
| 3 | Low | Sources rule vs. separate-column mode | spreadsheet-format.md |
| 4 | Low | Architecture diagram says N=2–10, can be 1 | SKILL.md |
| 5 | Medium | Merge rules unclear for 1–2 question RFPs | SKILL.md |
| 6 | Low | Persona "you write" vs. subagents write | SKILL.md |
| 7 | Low | Subagent prompt mentions "sheet" (they have no access) | subagent-prompt.md |
| 8 | Low | Step 3 vs. Phase order | SKILL.md |
| 9 | Low | sample-qa not referenced | SKILL.md |
| 10 | Low | Hardcoded numbers in Quick Ref / Pre-Flight | SKILL.md |
| 11 | Info | Subagent Sources format—likely intentional | subagent-prompt.md |
