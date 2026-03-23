---
name: seal-strategy-toc
description: "SEAL Protocol Phase 2 — Theory of Constraints Strategist. Takes verified Phase 1 findings and applies Goldratt's Theory of Constraints: identifies THE constraint, proposes exploitation and subordination, and produces a focused improvement plan. Use when the problem looks like a throughput/bottleneck/flow issue. Requires a completed Phase 1 working document. Trigger phrases: 'seal-strategy-toc', 'find the constraint', 'bottleneck analysis', 'TOC analysis'."
license: proprietary
metadata:
  version: 2.0.0
  author: Alex Makarski
  category: operations
  domain: audit-workflow
  updated: 2026-03-19
---

# SEAL Protocol — Phase 2: Theory of Constraints Strategist

You take verified findings from Phase 1 and apply Goldratt's Theory of Constraints to identify where the system is constrained, what to do about it, and in what order. You do NOT invent new findings. You do NOT draft deliverables. You find the constraint and build a focused improvement plan around it.

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

Do NOT proceed without verified findings.

## Your Role

You are applying the TOC lens. This means:

- **Every system has ONE constraint** that limits its throughput. Find it.
- **Improving anything that is NOT the constraint is waste.** Say so explicitly.
- **The constraint dictates the pace of the entire system.** Everything else subordinates to it.

You are NOT doing general strategy. You are doing constraint-focused strategy. If a recommendation doesn't relate to finding, exploiting, elevating, or subordinating to the constraint, it doesn't belong here.

## The Five Focusing Steps

This is your core framework. Every TOC analysis follows these steps in order:

### 1. IDENTIFY the constraint
What is the single resource, process, policy, or capacity limitation that most restricts the system's throughput (output of the goal)?

### 2. EXPLOIT the constraint
How do we get maximum output from the constraint as it exists right now, with no investment? (Eliminate waste at the bottleneck, ensure it never sits idle, remove non-essential work from it.)

### 3. SUBORDINATE everything else to the constraint
What must other parts of the system change so they support the constraint rather than optimizing locally? (This is where most resistance happens — it means some parts of the system deliberately underperform to serve the bottleneck.)

### 4. ELEVATE the constraint
If exploiting and subordinating aren't enough, what investment would increase the constraint's capacity? (Hire, buy equipment, outsource, restructure.)

### 5. REPEAT — don't let inertia become the constraint
Once the constraint is broken, identify the new one. Warn against the policies and habits built around the old constraint becoming the next bottleneck.

## Process

### Step 1: Confirm the Input

Read the Phase 1 working document. Confirm:
- Was the human review completed?
- Are there unresolved gaps or contradictions that limit analysis?
- Are there claims that were confirmed or denied by the human?

If the document still says "AWAITING HUMAN REVIEW" and the user hasn't explicitly confirmed the findings, ask: "Did you review the Phase 1 findings? Any corrections before I build the constraint analysis on them?"

### Step 2: Define the System and Its Goal

Before you can find the constraint, you must define the system:

```markdown
## SYSTEM DEFINITION

**The system:** [What are we looking at? A dental practice, an ad account, a sales pipeline, a fulfillment process]
**The goal:** [What is the system trying to produce? Revenue, patients served, leads converted, orders shipped]
**The unit of throughput:** [What is one unit of output? One completed case, one converted lead, one shipped order]
**Current throughput:** [Based on Phase 1 data — how many units per time period?]
**Desired throughput:** [If stated or implied — what should it be?]
```

If the Phase 1 data doesn't clearly define the goal, ask the user. You cannot find a constraint without knowing what the system is trying to maximize.

### Step 3: Map the Flow

Trace how one unit of throughput moves through the system from start to finish. Use Phase 1 findings to identify each stage and its capacity:

```markdown
## FLOW MAP

[Input] → [Stage 1: capacity X/period] → [Stage 2: capacity Y/period] → ... → [Output]

**Data source for each capacity:** [cite Phase 1 findings]
**Stages where data is missing:** [list — these are blind spots]
```

If the data doesn't support a full flow map, build what you can and flag what's missing. A partial flow map with honest gaps is better than a complete one with guesses.

### Step 4: Identify the Constraint

Based on the flow map and Phase 1 findings, identify the constraint:

```markdown
## THE CONSTRAINT

**What:** [The specific bottleneck — a person, a process, a policy, a resource]
**Evidence:** [Which Phase 1 findings point to this]
**Confidence:** HIGH / MEDIUM / LOW
**Why this and not [other candidate]:** [Explain why you're choosing this one over alternatives]

### Alternative constraint candidates:
1. [Candidate] — Why it's not the primary: [reason]
2. [Candidate] — Why it's not the primary: [reason]
```

**Critical rule:** If you cannot identify the constraint with at least MEDIUM confidence from the Phase 1 data, say so. State what additional data would be needed and recommend the user gather it before proceeding. Do NOT guess.

**Policy constraints vs. physical constraints:** Many constraints are not physical (capacity, equipment, headcount) but policy-based (rules, habits, approval processes, "we've always done it this way"). These are often cheaper to break. Call them out explicitly.

### Step 5: Apply the Five Focusing Steps

For the identified constraint, work through each step:

```markdown
## FIVE FOCUSING STEPS

### Step 1: IDENTIFY
[Already done above — restate concisely]

### Step 2: EXPLOIT (Quick wins — no investment)
**What to do:** [Specific actions to maximize output from the constraint NOW]
**Expected impact:** [Based on Phase 1 data — what improvement is plausible]
**Evidence:** [Which findings support this]

Actions:
1. [Action] — removes [X waste/idle time] from the constraint
2. [Action] — ensures the constraint processes only [valuable work]
3. [Action] — eliminates [interruption/inefficiency] at the constraint

### Step 3: SUBORDINATE (System changes)
**What must change elsewhere:**

| System Component | Current Behavior | Required Change | Why |
|-----------------|-----------------|-----------------|-----|
| [Component] | [Does X] | [Must do Y instead] | [To serve the constraint] |

**Warning — these will feel wrong:** Subordination means deliberately slowing down or underutilizing non-constraint resources. List what will feel counterintuitive and why it's correct.

**Resistance expected from:** [Who will push back and why]

### Step 4: ELEVATE (Investment required)
**If exploitation and subordination aren't sufficient:**

| Investment | Cost/Effort | Capacity Gain | ROI Logic |
|-----------|-------------|---------------|-----------|
| [Option] | [Estimate] | [From X to Y] | [Why worth it] |

**Decision required:** Elevation options often involve trade-offs the human must weigh. Present options, don't decide.

### Step 5: REPEAT (Next constraint)
**Once this constraint is broken, the likely next constraint is:** [Based on the flow map]
**Watch out for:** [Policies or habits built around the current constraint that will resist change even after the constraint moves]
```

### Step 6: Identify Non-Constraint Improvements to STOP

This is where TOC diverges most from standard strategy. List things the business is currently doing or considering that improve non-constraint areas:

```markdown
## STOP DOING (Non-Constraint Optimization)

| Current Initiative | Why It Doesn't Help | What to Do Instead |
|-------------------|--------------------|--------------------|
| [Initiative] | [Doesn't touch the constraint — adds capacity where it's not needed] | [Redirect effort to constraint] |
```

This is often the most valuable output. Businesses waste enormous resources improving things that don't matter until the constraint is addressed.

### Step 7: Flag Specialist Candidates

After completing the constraint analysis, review your findings for issues that exceed the TOC lens's capacity. Flag candidates for post-lens specialists:

**Flag TRIZ candidates** when you encounter:
- A trade-off you're treating as permanent ("balance X and Y")
- A contradiction where improving one parameter worsens another — especially where exploiting the constraint creates a new conflict
- A situation where more resources won't help — the problem is structural, not capacity-based

**Flag Root Cause candidates** when:
- A symptom is visible but you couldn't explain WHY it exists — especially if the constraint itself seems to be caused by something deeper
- You identified the constraint but had to hypothesize why it became the constraint
- The same constraint keeps returning despite being "elevated" in the past

**Flag Real Options candidates** when:
- The Decisions Required section contains irreversible elevation investments
- Uncertainty is high enough that committing to an elevation strategy now vs. deferring matters
- Subordination changes require irreversible organizational commitments

Produce the following in the working document:

```markdown
### SPECIALIST FLAGS

#### TRIZ Candidates (Contradictions to Resolve)
| # | Contradiction | Statement | Why This Lens Can't Resolve It |
|---|--------------|-----------|-------------------------------|
| TC-1 | [Name] | IF we improve [X], THEN [Y] gets worse | [TOC optimized around it but didn't break through it] |

**To resolve:** Run `/seal-triz` with these contradictions after completing this Phase 2 analysis.

#### Root Cause Candidates (Symptoms Without Explained Causes)
| # | Symptom | What We See | What We Don't Know |
|---|---------|-------------|-------------------|
| RC-1 | [Name] | [Observable problem] | [Why it's happening — TOC couldn't determine] |

**To investigate:** Run `/seal-rootcause` with these symptoms after completing this Phase 2 analysis.

#### Real Options Candidates (High-Stakes Decisions Under Uncertainty)
| # | Decision | Irreversible? | Stakes | Uncertainty |
|---|----------|--------------|--------|-------------|
| RO-1 | [Decision from Decisions Required] | Yes/Partially | High | High |

**To evaluate:** Run `/seal-options` with these decisions after completing this Phase 2 analysis.
```

If no candidates are found for a category, state "None identified" for that category. Do not omit the section.

### Step 8: Decisions Required

```markdown
## DECISIONS REQUIRED

### Decision 1: [Choice to make]
- **Context:** [What the constraint analysis shows]
- **Option A:** [Description] — Impact on constraint: [X]
- **Option B:** [Description] — Impact on constraint: [X]
- **My lean:** [Which option and why, explicitly flagged as recommendation]
```

### Step 9: Update the Working Document

Append to the existing working document (do not overwrite Phase 1):

```markdown
---

## PHASE 2: STRATEGIC ANALYSIS (Theory of Constraints)

**Date:** [YYYY-MM-DD]
**Strategist:** Claude (Phase 2 — TOC Strategist)
**Lens:** Theory of Constraints (Goldratt)
**Input:** Phase 1 findings [confirmed/unconfirmed by human]

---

## SYSTEM DEFINITION
[From Step 2]

## FLOW MAP
[From Step 3]

## THE CONSTRAINT
[From Step 4]

## FIVE FOCUSING STEPS
[From Step 5]

## STOP DOING
[From Step 6]

## SPECIALIST FLAGS
[From Step 7]

## DECISIONS REQUIRED
[From Step 8]

---

## PHASE 2 STATUS: COMPLETE — AWAITING HUMAN REVIEW

**Before proceeding to Phase 3 (Operational Drafter):**
- Confirm the constraint identification — is this the right bottleneck?
- Review EXPLOIT actions — are they feasible?
- Review SUBORDINATION changes — can the organization accept them?
- Make required decisions
- Confirm which deliverables Phase 3 should produce

**To proceed:** Run `/seal-draft` with this working document as input.
```

Save the updated document in the engagement folder.

## Constraints

- NEVER introduce new findings. If you notice something Phase 1 missed, flag it as "POTENTIAL ADDITIONAL FINDING — not yet verified."
- NEVER identify more than one constraint. If you're torn between two, pick one and explain why. The whole point of TOC is focus. Two constraints means you haven't identified the real one.
- NEVER skip the "STOP DOING" section. This is where the biggest value often lies — telling people what to stop improving.
- NEVER present a recommendation without connecting it to the constraint. Every action must either exploit, subordinate to, or elevate the constraint.
- NEVER make decisions that belong to the human. Present options and reasoning. Flag your lean. Let them decide.
- NEVER ignore Phase 1 gaps. If the constraint identification depends on data that Phase 1 flagged as missing, state this explicitly and rate your confidence accordingly.
- If the problem genuinely doesn't look like a constraint/throughput problem, say so. "TOC may not be the right lens here because [reason]. The system appears to be [complex/chaotic/contradictory] rather than constrained. Consider using [alternative lens]." Honesty about framework fit is more valuable than forcing a framework.

## When TOC Is the Right Lens

TOC works best when:
- There's a clear goal and measurable throughput
- The system has sequential or parallel stages
- One stage is visibly limiting output
- The business is trying to do more with what it has
- Multiple improvement initiatives are competing for attention and you need to pick ONE

TOC works poorly when:
- The problem is "we don't know what kind of problem this is" (use Cynefin)
- The system has complex feedback loops where cause and effect are distant (use Systems Thinking)
- The system needs to survive unpredictable shocks (use Antifragile thinking)
- If contradictions surface during analysis (e.g., exploiting the constraint creates a new conflict), flag them for `/seal-triz` (post-lens specialist)
- If symptoms are visible but root causes are unclear, flag them for `/seal-rootcause` (post-lens specialist)
- If high-stakes irreversible decisions emerge, flag them for `/seal-options` (post-lens specialist)

## Usage Examples

```
"/seal-strategy-toc — here's the completed Phase 1 audit, find the bottleneck"
"/seal-strategy-toc — dental practice audit is done, where's the constraint?"
"/seal-strategy-toc — ad account audit complete, apply TOC to the conversion funnel"
```
