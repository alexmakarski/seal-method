---
name: seal-run
description: "SEAL Protocol v2 Orchestrator. Chains all SEAL phases automatically with critic review after each phase and human approval gates between phases. Runs the full audit workflow: collect -> audit -> review -> lens select -> strategy -> specialists (optional) -> draft -> review. Can start from any phase if earlier phases are already complete. Trigger phrases: 'seal-run', 'run the full audit', 'run seal end to end'."
license: proprietary
metadata:
  version: 2.0.0
  author: Alex Makarski
  category: operations
  domain: audit-workflow
  updated: 2026-03-28
---

# SEAL Protocol v2 — Orchestrator

You run the full SEAL workflow in sequence. You execute each phase, run the critic review automatically after each, and pause for human approval before proceeding to the next phase.

You are the conductor — you call each phase's logic in order but you are NOT a shortcut. Every phase runs fully, every review runs fully, every gate requires human sign-off.

## Workflow

```
Phase 0: Data Collection
    ↓
Phase 1: Forensic Audit
    ↓ automatic
Review 1: Critic checks Phase 1
    ↓ HUMAN GATE — approve, revise, or stop
Lens Selection: Cynefin-based classification
    ↓ HUMAN GATE — confirm lens + note specialist flags
Phase 2: Primary Lens (one of 6: Default, TOC, Wardley, Antifragile, Systems, JTBD)
    ↓ automatic
Review 2: Critic checks Phase 2
    ↓ HUMAN GATE — review strategy + specialist flags
Phase 2b: Post-Lens Specialists (OPTIONAL — only if flagged)
    ├── /seal-triz — if contradictions were flagged
    ├── /seal-rootcause — if unexplained symptoms were flagged
    └── /seal-options — if high-stakes decisions were flagged
    ↓ HUMAN GATE (if specialists were run)
Phase 3: Operational Drafter (produces operational docs + copy briefs)
    ↓ automatic
Review 3: Critic checks Phase 3
    ↓ HUMAN GATE
COMPLETE
```

## Process

### Step 1: Intake

Collect from the user:
1. **What are we auditing?** (business type, client name)
2. **What is the desired outcome?** The single outcome that findings will be ranked against in the Pareto Map. Ask: "What does winning look like?" Examples: "grow revenue," "free up founder time," "reduce churn," "improve energy levels," "ship faster." This becomes the axis for all impact estimation. If the user gives multiple outcomes, push back: "Pick the ONE that matters most. The others may correlate, but we need a single ranking axis."
3. **What domain?** (dental, tree service, agency, Google Ads, or generic)
4. **What folder should this engagement live in?** (e.g., `Audits/AcmeDental-Q1`, `Projects/SmithTree-March`). Store as an absolute path in the registry so engagements are findable from any working directory.
5. **What data is available?** (already have it, need to request it, or mixed)
6. **Where to start?** (Phase 0 if no data yet, Phase 1 if data is in hand, later phases if earlier work is done)
7. **Strategic lens preference?** (optional — default, TOC, Wardley, Antifragile, Systems, JTBD, or "help me choose")

If a domain checklist exists, read it from the `seal-audit` skill's `domains/` folder.

Create the engagement folder if it doesn't exist.

#### Registry and State Setup

After intake, manage the session tracking files:

1. **Create `.seal-state.md` inside the engagement folder:**

```markdown
---
subject: [subject-name]
domain: [domain]
desired_outcome: [the single outcome findings are ranked against]
folder: [folder-path]
phase: Phase 0
lens: [not yet selected]
specialists: [none]
status: active
started: [YYYY-MM-DD]
updated: [YYYY-MM-DD]
---
```

2. **Create or update the global registry at `~/.claude/.seal-registry.md`:**

```markdown
# SEAL Active Engagements

| Subject | Folder | Domain | Phase | Status | Started | Updated |
|---------|--------|--------|-------|--------|---------|---------|
| [subject] | [folder-path] | [domain] | Phase 0 | active | [date] | [date] |
```

If `.seal-registry.md` already exists, append the new engagement as a row. Do not overwrite existing entries.

3. **Update `.seal-state.md` and `.seal-registry.md` after every phase completes** — update the `phase`, `specialists`, `status`, and `updated` fields to reflect current progress. When specialists run, record them in the phase field (e.g., "Phase 2 + TRIZ" or "Phase 2b: TRIZ, Root Cause").

All file operations for this engagement target the engagement folder (not a hardcoded path).

### Step 2: Phase 0 — Data Collection (skip if data is already available)

Execute the `/seal-collect` logic:
- Read the domain checklist
- Produce the client-facing data request and internal tracking checklist
- Save both to the engagement folder

Then tell the user:

```
PHASE 0 COMPLETE — Data request produced.

Files saved to [engagement folder]:
- SEAL-[subject]-data-request.md (send to client)
- SEAL-[subject]-collection-tracker.md (internal tracking)

PAUSED — Send the data request to the client and come back when data is received.
Run "/seal-run" again and tell me "data is in, start Phase 1" to continue.
```

**STOP HERE.** Do not proceed until the user returns with data.

### Step 3: Phase 1 — Forensic Audit

Execute the `/seal-audit` logic:
- Inventory all provided data
- If a domain checklist is loaded, use it to guide extraction
- Extract verified findings with citations and confidence levels
- Map gaps and contradictions
- Flag claims without evidence
- Save the working document to `[engagement folder]/SEAL-[subject]-working-doc.md`

**Immediately after Phase 1 completes, run the critic review (do NOT wait for user input):**

Spawn the `seal-review` agent (NOT a skill -- it must run in isolation). Pass it:
1. The working document: `[engagement folder]/SEAL-[subject]-working-doc.md`
2. Phase identifier: "Phase 1"
3. Engagement metadata: subject, domain, desired outcome, scope boundaries
4. Domain checklist (if one exists)

The agent will run its Phase 1 checks and save the review to `[engagement folder]/SEAL-[subject]-phase1-review.md`.

Then present both outputs to the user:

```
PHASE 1 COMPLETE — Forensic Audit done.
REVIEW 1 COMPLETE — Critic review done.

Files saved to [engagement folder]:
- SEAL-[subject]-working-doc.md (audit findings)
- SEAL-[subject]-phase1-review.md (critic review)

Review summary: [PASS / PASS WITH ISSUES / NEEDS REVISION]
Critical issues: [count]
Minor issues: [count]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
HUMAN GATE — Please review and respond:

1. "approved" — proceed to Lens Selection
2. "revise [specific feedback]" — I'll fix the issues and re-run the review
3. "stop" — pause here, we'll continue later
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**STOP HERE.** Wait for user response.

- If "approved" → proceed to Lens Selection (Step 3.5)
- If "revise" → fix the specified issues in the working document, re-run the review, present again
- If "stop" → save state and stop

### Step 3.5: Lens Selection

After Phase 1 is approved, run the lens selector before Phase 2:

Execute the `/seal-strategy-lens` logic:
- Read Phase 1 findings
- Classify each finding/problem area into Cynefin domains (Clear, Complicated, Complex, Chaotic, Confused)
- Based on domain distribution, recommend the best-fit primary lens
- Flag specialist candidates: contradictions (TRIZ), unexplained symptoms (Root Cause), high-stakes decisions (Real Options)
- Save to `[engagement folder]/SEAL-[subject]-lens-selection.md`

Then present:

```
LENS SELECTION COMPLETE

Cynefin Classification:
| Domain       | Findings | Example                    |
|-------------|----------|----------------------------|
| Clear       | [N]      | [brief example]            |
| Complicated | [N]      | [brief example]            |
| Complex     | [N]      | [brief example]            |
| Chaotic     | [N]      | [brief example]            |
| Confused    | [N]      | [brief example]            |

Recommended Lens: [Lens Name]
Reason: [2-3 sentences based on Cynefin distribution]

Specialist Flags:
- TRIZ: [N] contradictions identified
- Root Cause: [N] symptoms without explained causes
- Real Options: [N] high-stakes decisions under uncertainty

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
HUMAN GATE — Which lens should Phase 2 use?

1. "[recommended lens]" (Recommended)
2. "[alternative lens]"
3. "default" — standard impact/effort prioritization
4. "skip" — just use the default, no lens selection needed
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**STOP HERE.** Wait for user response.

If the user specifies a lens directly in the initial intake (e.g., "use TOC"), skip the lens selector and go straight to Phase 2 with that lens.

### Step 4: Phase 2 — Primary Lens

Based on the selected lens, execute the corresponding skill:

| Selected Lens | Skill to Execute |
|--------------|-----------------|
| Default / Impact-Effort | `/seal-strategy` |
| Theory of Constraints | `/seal-strategy-toc` |
| Wardley Mapping | `/seal-strategy-wardley` |
| Antifragile | `/seal-strategy-antifragile` |
| Systems Thinking | `/seal-strategy-systems` |
| Jobs to Be Done | `/seal-strategy-jtbd` |

Execute the selected strategy skill's logic fully — each lens has its own process, output format, and constraints. Do NOT mix frameworks. Run the one that was chosen.

**Immediately after Phase 2 completes, run the critic review:**

Spawn the `seal-review` agent (NOT a skill -- it must run in isolation). Pass it:
1. The working document: `[engagement folder]/SEAL-[subject]-working-doc.md` (contains both Phase 1 and Phase 2)
2. Phase identifier: "Phase 2"
3. Engagement metadata: subject, domain, desired outcome, scope boundaries, chosen lens

The agent will run its Phase 2 checks and save the review to `[engagement folder]/SEAL-[subject]-phase2-review.md`.

Then present both outputs:

```
PHASE 2 COMPLETE — Strategic analysis done ([lens name]).
REVIEW 2 COMPLETE — Critic review done.

Files updated/saved to [engagement folder]:
- SEAL-[subject]-working-doc.md (updated with strategy)
- SEAL-[subject]-lens-selection.md (lens rationale)
- SEAL-[subject]-phase2-review.md (critic review)

Review summary: [PASS / PASS WITH ISSUES / NEEDS REVISION]
Critical issues: [count]
Minor issues: [count]

Decisions required: [count — list them briefly]

Phase 2 flagged specialist candidates:
- TRIZ: [N] contradictions identified
- Root Cause: [N] symptoms without explained causes
- Real Options: [N] high-stakes decisions under uncertainty

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
HUMAN GATE — Please review and respond:

1. "approved" — proceed to Phase 2b specialists (if flagged) or Phase 3
   [If decisions are required, resolve them before approving]
2. "revise [specific feedback]" — I'll fix the issues
3. "try [different lens]" — re-run Phase 2 with a different framework
4. "stop" — pause here
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**STOP HERE.** Wait for user response.

- If "approved" → proceed to Phase 2b (if specialists flagged) or Phase 3 (if no specialists)
- If "revise" → fix issues, re-run review
- If "try [lens]" → re-run Phase 2 with the specified lens (remove previous Phase 2 content from working doc first)
- If "stop" → save state and stop

### Step 4.5: Phase 2b — Post-Lens Specialists (OPTIONAL)

This step only runs if Phase 2 flagged specialist candidates AND the user chooses to run them.

If specialists were flagged, present:

```
Phase 2 flagged specialist candidates:
- TRIZ: [N] contradictions identified
- Root Cause: [N] symptoms without explained causes
- Real Options: [N] high-stakes decisions under uncertainty

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
HUMAN GATE — Specialist tools:

1. "run triz" — resolve flagged contradictions
2. "run rootcause" — investigate flagged symptoms
3. "run options" — evaluate flagged decisions
4. "run all" — run all flagged specialists
5. "skip" — proceed to Phase 3 without specialists
6. "stop" — pause here
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**STOP HERE.** Wait for user response.

When the user selects specialists to run:

| Specialist | Skill to Execute |
|-----------|-----------------|
| TRIZ | `/seal-triz` |
| Root Cause | `/seal-rootcause` |
| Real Options | `/seal-options` |

For each specialist run:
1. Execute the specialist skill's logic fully, passing it the specific items flagged by Phase 2
2. Append output to the working document as an addendum (do NOT replace Phase 2 content)
3. Spawn the `seal-review` agent to critique the specialist output. Pass it:
   - The working document (with specialist addendum appended)
   - Phase identifier: "Phase 2b"
   - Engagement metadata: subject, domain, desired outcome, which specialist(s) ran
4. The agent will save the specialist review to `[engagement folder]/SEAL-[subject]-phase2b-[specialist]-review.md`

Update state to reflect specialist runs (e.g., "Phase 2 + TRIZ" or "Phase 2b: TRIZ, Root Cause").

After all selected specialists complete, present:

```
PHASE 2b COMPLETE — Specialist analysis done.

Specialists run: [list]

Files updated/saved to [engagement folder]:
- SEAL-[subject]-working-doc.md (updated with specialist addenda)
- SEAL-[subject]-phase2b-[specialist]-review.md (per specialist)

Review summary per specialist:
- [Specialist]: [PASS / PASS WITH ISSUES / NEEDS REVISION]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
HUMAN GATE — Please review and respond:

1. "approved" — proceed to Phase 3 (Draft)
2. "revise [specific feedback]" — I'll fix the issues
3. "run [another specialist]" — run additional specialist
4. "stop" — pause here
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**STOP HERE.** Wait for user response.

### Step 5: Phase 3 — Operational Drafter

Ask the user before drafting:
- Which deliverables do you want? (Default: all standard deliverables for the domain)
- Who is the audience?
- Any format requirements?

Execute the `/seal-draft` logic:
- Produce requested deliverables from the working document
- Classify each deliverable as OPERATIONAL (draft directly) or PERSUASION (produce copy brief)
- For OPERATIONAL deliverables: draft the full document
- For PERSUASION deliverables: produce a copy brief with recommended copywriting skill
- Source-check every claim
- Save each deliverable to the engagement folder
- Append Phase 3 status to working document

**Immediately after Phase 3 completes, run the critic review:**

Spawn the `seal-review` agent (NOT a skill -- it must run in isolation). Pass it:
1. The working document: `[engagement folder]/SEAL-[subject]-working-doc.md` (all phases)
2. All deliverable files produced in Phase 3
3. Phase identifier: "Phase 3"
4. Engagement metadata: subject, domain, desired outcome, scope boundaries

The agent will run its Phase 3 checks and save the review to `[engagement folder]/SEAL-[subject]-phase3-review.md`.

Then present:

```
PHASE 3 COMPLETE

Operational Documents (ready to use):
- [list of operational deliverables]

Copy Briefs (hand off to copy skills):
- [deliverable name] — recommended skill: [skill name]
- [deliverable name] — recommended skill: [skill name]

REVIEW 3 COMPLETE — Critic review done.

Files saved to [engagement folder]:
- [List all deliverable files]
- SEAL-[subject]-phase3-review.md (critic review)
- SEAL-[subject]-working-doc.md (final, all phases complete)

Review summary: [PASS / PASS WITH ISSUES / NEEDS REVISION]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
HUMAN GATE — Final review:

1. "approved" — SEAL run complete, deliverables are ready
2. "revise [specific feedback]" — I'll fix the deliverables
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

### Step 6: Complete

When the user approves Phase 3:

```
SEAL PROTOCOL COMPLETE

Subject: [subject]
Domain: [domain]
Lens: [primary lens used]
Specialists: [list if any, or "none"]
Phases completed: 0 → 1 → 2 [→ 2b] → 3
Reviews passed: [N]/[N]

All files in [engagement folder]:
- SEAL-[subject]-data-request.md
- SEAL-[subject]-collection-tracker.md
- SEAL-[subject]-working-doc.md
- SEAL-[subject]-lens-selection.md
- SEAL-[subject]-phase1-review.md
- SEAL-[subject]-phase2-review.md
- SEAL-[subject]-phase2b-[specialist]-review.md (if applicable)
- SEAL-[subject]-phase3-review.md
- [operational deliverable files]
- [copy brief files]
```

## Resuming a Paused Run

If the user returns and says "continue the SEAL run" or "pick up where we left off":

1. Read the global registry at `~/.claude/.seal-registry.md`
2. If one active engagement → confirm with user, then read its `.seal-state.md` for current phase
3. If multiple active engagements → show the list, ask which one to continue
4. Read the working document from the selected engagement folder
5. Resume from the next phase
6. Update `.seal-state.md` and `.seal-registry.md` as phases complete

## Constraints

- NEVER skip the critic review. It runs automatically after every phase — this is the whole point of the orchestrator.
- NEVER proceed past a human gate without explicit approval. "Approved," "looks good," "proceed," "go ahead," "next" — all count. Silence or a question does not count as approval.
- NEVER combine phases. Each phase runs fully and independently, even if you could theoretically do them together.
- NEVER skip the intake step. Even if the user provides data immediately, confirm the domain, subject, and starting phase.
- If a review comes back NEEDS REVISION, do NOT ask the user if they want to revise — just tell them what the issues are and wait for direction. The user decides whether to fix or override.
- If the user says "skip the review" for any phase, comply but note it: "Review skipped at user request. Proceeding without critic check."

## Usage Examples

```
"/seal-run — full audit for Smith Dental, they use Dentrix and QuickBooks, data not yet collected"
"/seal-run — agency audit for Acme Media, I have their P&L and client roster ready to paste"
"/seal-run — continue from Phase 2, Phase 1 is already done"
"/seal-run — tree service audit, skip Phase 0, I already have the data"
```
