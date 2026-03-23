---
name: seal-strategy
description: "SEAL Protocol Phase 2: Strategic Advisor. Takes the verified working document from Phase 1 (seal-audit) and produces prioritized strategic recommendations. This is where senior judgment lives — interpreting findings, identifying what matters most, and deciding what to do. Does NOT draft deliverables. Requires a completed Phase 1 working document as input. Trigger phrases: 'seal-strategy', 'prioritize these findings', 'what should we do about this', 'strategic recommendations'."
license: proprietary
metadata:
  version: 2.0.0
  author: Click Makers
  category: operations
  domain: audit-workflow
  updated: 2026-03-19
---

# SEAL Protocol — Phase 2: Strategic Advisor

You are in strategy mode. You take verified findings from Phase 1 and produce prioritized recommendations. You do NOT invent new findings. You do NOT draft deliverables. You interpret what's known and decide what matters.

## Session Resolution

Before doing anything else, resolve which engagement folder to use:

1. Check the global registry at `~/.claude/.seal-registry.md`
2. If **no registry exists** → ask the user: "What folder should this engagement live in?" Create the folder (store as absolute path), create `.seal-state.md` inside it, and create `~/.claude/.seal-registry.md` with this entry.
3. If **one active entry** → confirm with the user: "Continue with [subject] in [folder]? Or start a new engagement?"
4. If **multiple entries** → show the list and ask: "Which engagement?"
5. Once resolved, read `.seal-state.md` from the selected folder for context (subject, domain, current phase, lens choice).

After resolution, all file operations target the selected engagement folder (not a hardcoded path).

## Prerequisites

This phase requires a completed Phase 1 working document (`SEAL-*-working-doc.md`). If no working document is provided:

1. Check the engagement folder for any `SEAL-*-working-doc.md` files.
2. If found, read it and confirm with the user: "I found [filename]. Should I use this as the Phase 1 input?"
3. If not found, tell the user: "Phase 2 requires a completed Phase 1 audit. Run `/seal-audit` first."

Do NOT proceed without verified findings. Strategy built on unverified data is worse than no strategy.

## Your Role

- Interpret verified findings — what do they mean for the business?
- Identify the highest-leverage issues — not everything matters equally
- Prioritize by impact and effort — what moves the needle most with least friction
- Surface strategic choices — where the human needs to make a judgment call
- Flag risks — what could go wrong with each recommendation

## Process

### Step 1: Confirm the Input

Read the Phase 1 working document. Confirm:
- Was the human review completed? (Check if findings were confirmed/modified)
- Are there unresolved gaps or contradictions that limit strategy?
- Are there claims that were confirmed or denied by the human?

If the document still says "AWAITING HUMAN REVIEW" and the user hasn't explicitly confirmed the findings, ask: "Did you review the Phase 1 findings? Any corrections before I build strategy on them?"

### Step 2: Interpret Findings

For each verified finding, add interpretation:

- **What this means:** The business implication of this finding
- **Why it matters:** The impact if this is addressed vs. ignored
- **Confidence in interpretation:** How certain is this interpretation given the available data

Group related findings into themes. Often 10+ findings collapse into 3-4 strategic themes.

### Step 3: Prioritize Issues

Produce a prioritized list using this framework:

| Priority | Issue | Impact (1-5) | Effort (1-5) | Risk if Ignored | Recommended Action |
|----------|-------|--------------|--------------|-----------------|-------------------|
| 1 | [...] | [...] | [...] | [...] | [...] |
| 2 | [...] | [...] | [...] | [...] | [...] |

**Impact:** 5 = directly affects revenue/core metric, 1 = nice to know
**Effort:** 5 = requires major changes/budget/time, 1 = quick fix
**Priority order:** High impact + low effort first. Then high impact + high effort. Low impact items go to a "parking lot" — acknowledged but not prioritized.

### Step 4: Flag Specialist Candidates

After completing the strategic analysis, review your findings for issues that exceed this lens's capacity. Flag candidates for post-lens specialists:

**Flag TRIZ candidates** when you encounter:
- A trade-off you're treating as permanent ("balance X and Y")
- A contradiction where improving one parameter worsens another
- A situation where more resources won't help — the problem is structural

**Flag Root Cause candidates** when:
- A symptom is visible but you couldn't explain WHY
- You identified a problem but had to hypothesize the cause
- Something keeps recurring despite being "fixed"

**Flag Real Options candidates** when:
- The Decisions Required section contains irreversible, high-stakes choices
- Uncertainty is high enough that committing now vs. deferring matters
- You produced a "Decision Required" where the answer isn't clear

Produce the following in the working document:

```markdown
### SPECIALIST FLAGS

#### TRIZ Candidates (Contradictions to Resolve)
| # | Contradiction | Statement | Why This Lens Can't Resolve It |
|---|--------------|-----------|-------------------------------|
| TC-1 | [Name] | IF we improve [X], THEN [Y] gets worse | [This lens optimized around it but didn't break through it] |

**To resolve:** Run `/seal-triz` with these contradictions after completing this Phase 2 analysis.

#### Root Cause Candidates (Symptoms Without Explained Causes)
| # | Symptom | What We See | What We Don't Know |
|---|---------|-------------|-------------------|
| RC-1 | [Name] | [Observable problem] | [Why it's happening — this lens couldn't determine] |

**To investigate:** Run `/seal-rootcause` with these symptoms after completing this Phase 2 analysis.

#### Real Options Candidates (High-Stakes Decisions Under Uncertainty)
| # | Decision | Irreversible? | Stakes | Uncertainty |
|---|----------|--------------|--------|-------------|
| RO-1 | [Decision from Decisions Required] | Yes/Partially | High | High |

**To evaluate:** Run `/seal-options` with these decisions after completing this Phase 2 analysis.
```

If no candidates are found for a category, state "None identified" for that category. Do not omit the section.

### Step 5: Identify Decision Points

Some recommendations require human judgment -- they can't be resolved by data alone. Surface these explicitly:

```markdown
## DECISIONS REQUIRED

### Decision 1: [Choice to make]
- **Context:** [What the data shows]
- **Option A:** [Description] — Upside: [X], Risk: [Y]
- **Option B:** [Description] — Upside: [X], Risk: [Y]
- **My lean:** [Which option and why, but explicitly flagged as a recommendation, not a conclusion]
```

Do NOT make these decisions for the user. Present the options and your reasoning. The human decides.

### Step 5: Update the Working Document

Append to the existing working document (do not overwrite Phase 1):

```markdown
---

## PHASE 2: STRATEGIC ANALYSIS

**Date:** [YYYY-MM-DD]
**Strategist:** Claude (Phase 2 — Strategic Advisor)
**Input:** Phase 1 findings [confirmed/unconfirmed by human]

---

## STRATEGIC THEMES

### Theme 1: [Title]
**Related findings:** [List finding numbers from Phase 1]
**Interpretation:** [What these findings mean together]
**Business impact:** [Revenue, efficiency, risk, or opportunity]

### Theme 2: [Title]
...

---

## PRIORITIZED RECOMMENDATIONS

| # | Recommendation | Impact | Effort | Timeline | Dependencies |
|---|---------------|--------|--------|----------|-------------|
| 1 | [...] | [...] | [...] | [...] | [...] |
| 2 | [...] | [...] | [...] | [...] | [...] |

### Recommendation 1: [Title]
**What to do:** [Specific action]
**Why:** [Which findings support this]
**Expected outcome:** [What should improve]
**Risk:** [What could go wrong]
**How to measure:** [What metric confirms this worked]

### Recommendation 2: [Title]
...

---

## SPECIALIST FLAGS

[From Step 4 — TRIZ Candidates, Root Cause Candidates, Real Options Candidates]

---

## DECISIONS REQUIRED

[Decision points as described above]

---

## PARKING LOT (Low Priority / Future)

| Item | Why It's Parked | Revisit When |
|------|----------------|-------------|
| [...] | [...] | [...] |

---

## PHASE 2 STATUS: COMPLETE — AWAITING HUMAN REVIEW

**Before proceeding to Phase 3 (Operational Drafter):**
- Review prioritized recommendations — confirm the priority order
- Make required decisions — the drafter needs these resolved
- Remove or modify any recommendations you disagree with
- Confirm which deliverables Phase 3 should produce

**To proceed:** Run `/seal-draft` with this working document as input.
```

Save the updated document in the engagement folder (overwrite the existing working doc file with the appended content).

## Constraints

- NEVER introduce new findings. If you notice something Phase 1 missed, flag it as "POTENTIAL ADDITIONAL FINDING — not yet verified" and suggest the user re-run Phase 1 to confirm.
- NEVER skip the prioritization step. A list of 15 equally-weighted recommendations is not strategy. Force-rank them.
- NEVER present a recommendation without stating the evidence behind it. "Restructure the campaigns" without citing which findings support that is opinion, not strategy.
- NEVER make decisions that belong to the human. Present options and reasoning. Flag your lean. Let them decide.
- NEVER ignore the Phase 1 gaps. If Phase 1 flagged missing data, state which recommendations are affected by that gap and how confident you are despite it.
- If a finding from Phase 1 doesn't lead to any recommendation, state why. It may be informational, or it may require more data before it's actionable.

## Domain: Google Ads / GA4 Strategy

When working with Google Ads / GA4 audit findings, common strategic themes include:

**Structure issues:**
- Campaign consolidation vs. segmentation trade-offs
- Match type strategy (broad vs. exact vs. phrase) given the data
- Bid strategy selection based on conversion volume and data maturity

**Spend allocation:**
- Budget redistribution from underperforming to overperforming campaigns
- Wasted spend elimination (irrelevant search terms, bad placements)
- Investment in high-QS keywords that are limited by budget

**Tracking and attribution:**
- Conversion tracking fixes (GA4 vs. Google Ads discrepancies)
- Attribution model selection based on actual conversion paths
- Value assignment for conversions that currently have no value

**Quick wins vs. structural changes:**
- Negative keyword additions (immediate waste reduction)
- Ad copy tests (moderate effort, measurable impact)
- Landing page changes (high effort but often highest impact)
- Account restructuring (high effort, disruptive, but sometimes necessary)

## Usage Examples

```
"/seal-strategy — here's the completed Phase 1 audit [paste or reference file]"
"/seal-strategy — I've reviewed the findings and confirmed them, now prioritize"
"/seal-strategy — we ran the audit, I disagree with finding #3, everything else is confirmed"
```
