# SEAL: Strategic Evidence Authority Ladder

## What It Is

SEAL is a multi-phase audit method that finds the vital few things that matter in any complex situation (the 80/20 of whatever outcome you care about) and backs them with verified evidence, not opinions. It replicates the authority hierarchy of a consulting team: analyst collecting data, manager reviewing their work, partner applying strategic judgment, specialists called in when needed, and back down to the team for deliverable production. Each rung of the ladder has strict constraints on what it's allowed to do, connected by quality gates and human approval points that prevent errors from compounding downstream.

It is not a prompt. It is a *workflow architecture* built from role-locked phases that mirror the consulting ladder. The minion collecting data cannot make strategic recommendations. The manager reviewing work cannot invent new findings. The partner applying strategy cannot fabricate evidence.

---

## The Core Workflow

```
Phase 0: Data Collection
    ↓
Phase 1: Forensic Audit + Pareto Map (80/20 ranking of all findings)
    ↓ (automatic)
Review 1: Critic checks Phase 1
    ↓ HUMAN GATE: approve, revise, or stop
Lens Selection: Cynefin-based domain classification + contradiction pre-scan
    ↓ HUMAN GATE: confirm lens + note specialist flags
Phase 2: Strategic Analysis (one of 6 primary lenses)
    ↓ (automatic)
Review 2: Critic checks Phase 2 + specialist flags
    ↓ HUMAN GATE: approve, review flags, decide on specialists
Phase 2b: Post-Lens Specialists (optional, only if flagged)
    ├── TRIZ: resolve contradictions the lens couldn't break
    ├── Root Cause: drill into symptoms the lens couldn't explain
    └── Real Options: evaluate decisions the lens couldn't settle
    ↓ HUMAN GATE (if specialists ran)
Phase 3: Operational Drafting + Copy Briefs
    ↓ (automatic)
Review 3: Critic checks Phase 3
    ↓ HUMAN GATE: approve or revise
COMPLETE
```

Each phase produces a persistent working document in the engagement folder. Each review runs automatically, so the human doesn't have to remember to request it. Each gate requires explicit human approval before the next phase starts. The run can be paused and resumed at any gate.

### The Phases

**Phase 0: Data Collection** (`/seal-collect`). Before analysis begins, the collector reads the domain checklist and produces a specific, actionable data request the client can follow. The request is organized by source system, prioritized by criticality, with export instructions. It also produces an internal tracking checklist. This phase prevents the most common audit failure: starting analysis on incomplete data.

**Phase 1: Forensic Audit** (`/seal-audit`). The auditor is in verification mode. It trusts nothing. It inventories what data is available, classifies source reliability into tiers, extracts verified findings with citations and confidence levels, maps gaps and contradictions, and flags claims without evidence. The auditor is *prohibited from recommending actions*. Its job is to say what IS, not what to DO. Every finding must cite its source; every confidence level must be justified; every statistic must trace to an attribution chain.

Phase 1 concludes with a **Pareto Map**, an 80/20 analysis that ranks all verified findings by their estimated impact on the engagement's stated desired outcome. The desired outcome is set during intake: "What does winning look like?" It can be revenue growth, time freed, churn reduced, energy improved, cycle time shortened. Any single outcome the person cares about. The Pareto Map estimates each finding's relative impact on that outcome (HIGH / MEDIUM / LOW, with magnitude where the data supports it), ranks them, and draws a line where a small number of findings account for a disproportionate share of total addressable impact. This is the "vital few," typically 3-5 findings out of 15-40, that should command attention before anything else. The Pareto Map is not a strategy or recommendation; it is a data-grounded ranking that Phase 2 uses as input. If no power law concentration exists (all findings have roughly equal impact), the map says so explicitly rather than forcing a pattern that isn't there.

**Lens Selection** (`/seal-strategy-lens`). After Phase 1 is approved, the lens selector uses Cynefin domain classification to route findings to the right primary lens. It also runs a contradiction pre-scan, identifying design contradictions (TRIZ candidates), unexplained symptoms (Root Cause candidates), and irreversible decisions under uncertainty (Real Options candidates). The selector routes to 6 primary lenses and flags up to 3 post-lens specialists. The human confirms the lens and reviews the specialist flags, or overrides either.

**Phase 2: Strategic Analysis** (one of 6 primary lens skills). The strategist takes verified findings and applies the selected framework. It interprets what the findings mean, identifies what matters most, prioritizes actions, and surfaces decisions that require human judgment. The strategist is *prohibited from inventing new findings*. If it notices something Phase 1 missed, it flags it rather than treating it as established fact. Each lens has its own process, output format, and constraints tailored to the framework. Each primary lens now includes a Specialist Flags step that explicitly identifies contradictions, unexplained symptoms, and high-stakes decisions that the lens encountered but couldn't resolve within its own framework.

**Phase 2b: Post-Lens Specialists** (`/seal-triz`, `/seal-rootcause`, `/seal-options`). Optional. When a primary lens flags issues it can't resolve, three specialist tools are available. TRIZ takes contradictions and applies a full inventive problem-solving methodology (40 business-adapted principles, a contradiction matrix, evolution patterns, and Su-Field analysis) to break through trade-offs rather than balancing them. Root Cause takes unexplained symptoms and drills down with 5 Whys, Ishikawa diagrams, and convergence analysis. Real Options takes high-stakes decisions and evaluates commit-vs-defer timing, designs probes, and sets kill criteria. These specialists don't replace the primary lens. They supplement it on specific sub-problems.

**Phase 3: Operational Drafting** (`/seal-draft`). The drafter takes confirmed findings (Phase 1) and approved strategy (Phase 2) and produces client-ready deliverables: executive summaries, detailed findings tables, action plans, slide deck briefs. The drafter is *prohibited from introducing new analysis or changing priorities*. Every number must trace to Phase 1; every recommendation must trace to Phase 2. If something doesn't trace back, it gets flagged rather than quietly included. For persuasion deliverables (landing page copy, talk scripts, email sequences, ad copy), Phase 3 produces a copy brief rather than attempting to write the copy itself. The brief contains everything a specialized copywriting skill needs: audience, job to be done, key messages, proof points, positioning, tone, CTA, and a recommended copy skill with reasoning. SEAL diagnoses and strategizes; it hands off to specialists for persuasion.

**The Critic** (`/seal-review`). Runs automatically after every phase, including specialists. It adapts its checks to the phase it's reviewing: citation checks and interpretation leak detection for Phase 1; evidence trail, prioritization quality, and specialist flag completeness for Phase 2; methodology and scope checks for Phase 2b specialists; source tracing and scope checks for Phase 3. The critic doesn't fix issues. It flags them with specific remediation instructions. The human decides whether to fix or override.

**The Orchestrator** (`/seal-run`). Chains all phases automatically, runs the critic after each, and enforces human gates between phases. Can start from any phase if earlier work is done. Manages the engagement folder, state file, and global registry. The orchestrator is a conductor, not a shortcut. Every phase runs fully, every review runs fully, every gate requires explicit sign-off.

### Session Management

SEAL supports parallel engagements through a two-layer tracking system:

- **Global registry** (`~/.claude/.seal-registry.md`) lists all active engagements with their folder paths, domains, current phase, and status. Any SEAL skill can find any engagement from any working directory.
- **Per-engagement state** (`.seal-state.md` inside each engagement folder) stores subject, domain, current phase, lens choice, and timestamps. Enables cross-skill handover within an engagement.

### Domain Checklists

Domain-specific checklists provide sector-specific intelligence for the audit phase: what data sources to look for, what metrics to extract with benchmarks, what contradictions are common, and what claims owners typically make without evidence. Currently available for dental practice, Google Ads, tree service, agency, tax discovery, and marketing data readiness audits. New domains are added by writing a single checklist file.

---

## Why It Works Better Than Naked Prompting

Naked prompting (giving an LLM a task in a single instruction and accepting the output) has five structural failure modes that SEAL is specifically designed to eliminate:

### 1. Blurred Roles Create Contaminated Output

When you ask an LLM to "audit this data and tell me what to do," it simultaneously tries to verify facts, interpret them, prioritize actions, and draft recommendations in a single pass. The result is a confident-sounding document where unverified claims get treated as facts, interpretations get presented as data, and recommendations appear without evidence trails.

**SEAL fix:** Each phase is role-locked. The auditor is prohibited from recommending. The strategist is prohibited from inventing new findings. The drafter is prohibited from changing priorities. The constraints are explicit: "If you catch yourself writing 'I recommend,' stop. You are in the wrong mode."

### 2. No Verification Layer

LLMs do not naturally distinguish between facts, claims, and assumptions. In a naked prompt, a statistic from a blog post with no attribution gets the same treatment as data from an official platform report. The model sounds equally confident about both.

**SEAL fix:** Phase 1 enforces a source reliability classification (Tier 1/2/3), a sole-source rule (single non-primary sources cannot produce verified findings), an attribution chain rule (stats without cited sources are flagged as Tier 3 regardless of who wrote them), and a platform currency rule (current-state claims must be verified against official docs, not LLM training data). These aren't suggestions. They're hard constraints the critic checks for.

### 3. No Error Correction Before Delivery

Naked prompting is single-pass. If the model makes a mistake in paragraph 3, that mistake propagates through every subsequent paragraph. The user is the only quality check, and they see the output only after it's complete.

**SEAL fix:** The critic (`/seal-review`) runs automatically after every phase, checking that phase's output against its own constraints. It catches interpretation leaks in audit findings, unsupported recommendations in strategy, and invented content in deliverables before the human ever sees the next phase. It flags specific issues with specific remediation instructions.

### 4. No Decision Separation

In a naked prompt, the model makes judgment calls silently, choosing which findings matter, which recommendations to prioritize, which trade-offs to resolve. The human has no visibility into these decisions and no opportunity to override them before they're baked into the output.

**SEAL fix:** Strategic decisions are surfaced explicitly as "DECISIONS REQUIRED" with options, trade-offs, and the model's stated lean. Human gates ensure no phase proceeds without explicit approval. The model presents options and reasoning; the human decides.

### 5. Context Decay Over Long Tasks

In a single long prompt, the model's attention to early instructions degrades as the output grows. By the time it's drafting the action plan, it may have forgotten constraints from the audit phase.

**SEAL fix:** Each phase is a separate invocation with its own skill file, its own constraints, and its own output document. The working document serves as the persistent state between phases, so the model reads the actual document rather than relying on its memory of what it said earlier. The orchestrator (`/seal-run`) manages the sequence but each phase runs independently.

---

## What Class of Problems SEAL Applies To

### Strong Fit

SEAL is designed for **analytical work where accuracy matters more than speed** and where **the cost of a wrong conclusion is high relative to the cost of being thorough.**

Specific problem classes:

- **Business audits** (financial, operational, marketing) where you need to establish ground truth from messy data before making recommendations
- **Account audits** (Google Ads, analytics platforms) where data is available but needs forensic verification before strategic advice
- **Due diligence** for evaluating a business, vendor, or partnership where you need verified facts separated from claims
- **Compliance reviews** where the distinction between "data shows X" and "we assume X" has real consequences
- **Complex consulting engagements** where the deliverable goes to a client and errors damage credibility
- **Multi-source investigations** where data comes from different systems that may contradict each other
- **Any situation where you've been burned by an LLM confidently stating something that turned out to be wrong.** SEAL's entire architecture is designed to prevent that specific failure mode.

The method is domain-extensible: domain checklists (currently dental practice, Google Ads, tree service, agency, tax discovery, and marketing data readiness) provide sector-specific data inventories, metric benchmarks, and common contradiction patterns. New domains are added by writing a new checklist file.

### Poor Fit

SEAL is the wrong tool when:

- **Speed matters more than accuracy.** SEAL is deliberately slow, with multiple phases, multiple reviews, multiple gates. If you need a quick answer, a naked prompt is faster and the accuracy trade-off may be acceptable.
- **The task is creative, not analytical.** Writing copy, brainstorming ideas, generating content. These don't benefit from forensic verification. There's nothing to audit.
- **The input is simple and unambiguous.** If someone gives you a clean spreadsheet and asks for a summary, you don't need a three-phase method with critic reviews. SEAL's overhead isn't justified.
- **There is no data.** SEAL is a data-processing pipeline. If the input is a question ("What's the best way to structure Google Ads campaigns?"), not a dataset, there's nothing for Phase 1 to verify.
- **The domain is well-understood and the answer is known.** If you're following a documented procedure, not analyzing whether the procedure is right, SEAL adds friction without value.
- **Real-time or interactive work.** Chat-based troubleshooting, pair programming, live Q&A. SEAL's gated phases assume you can pause and resume, not that you're in a live conversation.

### The Decision Rule

Use SEAL when:  **the cost of a wrong answer > the cost of being slow.**

Use naked prompting when: **the cost of being slow > the cost of a wrong answer.**

---

## How It Differs from "Just a Better Prompt"

SEAL is not a prompt engineering technique. It is a **process architecture** that constrains the model's behavior through:

1. **Role isolation.** Each phase has a persona with explicit prohibitions, not just instructions.
2. **Persistent state.** A working document that survives between phases, rather than relying on context window memory.
3. **Automated adversarial review.** The critic runs without being asked, checking the output against the phase's own rules.
4. **Human-in-the-loop gates.** Explicit pause points where the human reviews before the next phase uses the previous output as input.
5. **Pareto Map.** After extracting all findings, Phase 1 ranks them by estimated impact on the engagement's stated desired outcome and identifies the vital few that account for the majority of addressable impact. The desired outcome is defined at intake and can be anything (revenue, time, health, speed), making the method applicable to any domain, not just business.
6. **Framework selection.** The problem's shape determines which strategic lens is applied, rather than using a one-size-fits-all approach.
7. **Domain knowledge injection.** Domain checklists provide sector-specific intelligence without cluttering the core method.
8. **Resumability.** The run can be paused at any gate, data can be gathered externally, and the method picks up where it left off.
9. **Specialist handoff.** When a primary analysis hits a wall (a contradiction it can't break, a symptom it can't explain, a decision it can't evaluate), SEAL explicitly flags the issue and routes it to the right specialist tool rather than producing a mediocre compromise. And when a deliverable requires persuasion rather than analysis, SEAL produces a copy brief and hands off to specialized copywriting skills rather than attempting to write copy it's not built for.

A better prompt makes the model's single pass better. SEAL makes the model's output the product of multiple constrained passes, each checked against its own standards, with human judgment injected at critical decision points. The difference is architectural, not editorial.

---

## The Strategic Lenses

Phase 2 is where SEAL becomes adaptable. The strategic layer has a three-tier architecture:

- **Pre-Lens:** The Cynefin-based selector classifies findings by domain and routes to the right primary lens. It also runs a contradiction pre-scan, flagging issues that may need specialist attention after the primary analysis.
- **6 Primary Lenses (Phase 2):** Default (Impact/Effort), Theory of Constraints, Wardley Mapping, Antifragile, Systems Thinking, and Jobs to Be Done. Each applies a distinct framework to the verified findings and produces a complete strategic analysis, including explicit Specialist Flags for issues that exceeded its scope.
- **3 Post-Lens Specialists (Phase 2b):** TRIZ (contradiction resolution), Root Cause (symptom drilling), and Real Options (decision evaluation). These don't analyze the full findings. They take specific flagged sub-problems from a primary lens and resolve them with specialized methodology.

The key insight: **the same data produces fundamentally different recommendations depending on which lens you apply.** A dental practice audit analyzed through Theory of Constraints will focus on the single bottleneck limiting patient throughput. The same audit through Antifragile will focus on revenue concentration risk. The same audit through Jobs to Be Done will ask whether the practice is solving the right problem for its patients. None of these is wrong. They're answering different questions. The lens determines which question gets asked.

---

### 1. Default: Impact/Effort Prioritization

**Skill:** `/seal-strategy`
**Framework:** Standard strategic prioritization matrix
**Best for:** Straightforward operational audits where the findings are clear and the main question is "what order do we fix things in?"

The default lens groups findings into strategic themes, scores each recommendation by impact (1-5) and effort (1-5), force-ranks them, surfaces decisions that require human judgment, and parks low-priority items explicitly rather than dropping them.

**Use when:** Cause and effect are identifiable. The fixes are known. You need prioritization, not diagnosis.
**Don't use when:** The problem is ambiguous, systemic, or structural. A prioritized list of fixes won't help if you're fixing the wrong things.

---

### 2. Theory of Constraints (Goldratt)

**Skill:** `/seal-strategy-toc`
**Framework:** Goldratt's Five Focusing Steps
**Best for:** Throughput problems where one bottleneck limits the entire system's output.

TOC finds THE constraint, the single resource, process, or policy that limits throughput, then works through five steps: identify it, exploit it (maximize output with no investment), subordinate everything else to it (deliberately underperform elsewhere to serve the bottleneck), elevate it (invest if needed), and repeat when the constraint moves.

The most valuable output is often the "STOP DOING" section: things the business is currently improving that don't touch the constraint and are therefore wasted effort.

**Use when:** There's a measurable throughput goal, sequential stages, and one stage is visibly limiting output.
**Don't use when:** The problem is ambiguous (use Cynefin), has complex feedback loops (use Systems Thinking), or involves fundamental contradictions (use TRIZ).

---

### 3. Cynefin (Snowden)

**Skill:** `/seal-strategy-cynefin` (as primary lens) / also powers `/seal-strategy-lens` (as pre-lens selector)
**Framework:** Snowden's Cynefin Framework, five domains with distinct response patterns
**Best for:** Ambiguous problems where you don't know what kind of problem you're dealing with.

Cynefin now serves a dual role in SEAL. As the **lens selector**, it classifies Phase 1 findings by domain to route the engagement to the right primary lens. This happens automatically during Lens Selection. As a **primary lens**, it provides the full standalone analysis described below when the problem is genuinely ambiguous and domain classification itself is the highest-value output.

Cynefin classifies the problem into domains: Clear (apply best practice), Complicated (analyze with expertise), Complex (probe with safe-to-fail experiments), Chaotic (act immediately to stabilize), or Confused (break into parts and classify each). The classification itself IS the strategy. Once you know which domain you're in, the appropriate response pattern becomes clear.

Most business failures come from treating complex problems as complicated, assuming you can analyze your way to an answer when the system is actually emergent and unpredictable. Cynefin catches this.

**Use when:** Different stakeholders see the problem differently, previous interventions produced unexpected results, or the situation feels "messy."
**Don't use when:** The constraint is obvious (use TOC), the problem is clearly a feedback loop (use Systems Thinking), or you need to resolve specific contradictions (TRIZ specialist can handle those after your primary lens runs).

---

### 4. Systems Thinking (Meadows / Senge)

**Skill:** `/seal-strategy-systems`
**Framework:** System Dynamics: causal loops, stocks and flows, leverage points, system archetypes
**Best for:** Problems involving feedback loops, delays between cause and effect, fixes that backfire, or emergent behavior from interactions.

Systems Thinking maps the circular causality that linear analysis misses. It identifies reinforcing loops (growth engines or vicious cycles), balancing loops (natural governors), delays (where the time lag between action and result causes overreaction), and leverage points (where small changes produce disproportionate effects).

It matches findings against eight system archetypes (Fixes That Fail, Shifting the Burden, Limits to Growth, Tragedy of the Commons, Success to the Successful, Eroding Goals, Escalation, and Growth and Underinvestment), each with a known structural pattern and intervention strategy.

**Use when:** Fixes keep backfiring, problems keep recurring despite being "solved," or the system behaves in ways that no single cause explains.
**Don't use when:** The problem is a straightforward bottleneck (use TOC), the problem type is ambiguous (use Cynefin), or the problem involves fundamental contradictions (use TRIZ).

---

### 5. TRIZ (Altshuller), Post-Lens Specialist

**Skill:** `/seal-triz`
**Framework:** Theory of Inventive Problem Solving: contradiction resolution, inventive principles, ideality, evolution patterns
**Role:** Post-lens specialist. Takes contradictions flagged by a primary lens and resolves them. Not a peer lens; it doesn't analyze the full findings.

TRIZ activates when a primary lens identifies a contradiction it can't break within its own framework ("we need X but X causes Y") and flags it for specialist resolution. Its input is the specific contradiction, not the raw Phase 1 findings.

The full TRIZ sub-system includes: 40 Inventive Principles adapted from engineering for business context (Segmentation, Extraction, "The Other Way Around," Convert Harm to Benefit, Self-Service, Dynamization, Prior Action, and 33 more); a Contradiction Matrix that maps improving/worsening parameter pairs to the principles most likely to resolve them; Evolution Patterns that predict how business systems evolve toward ideality; Su-Field Analysis for modeling interactions between components; and Mini-ARIZ, a structured algorithm for the hardest contradictions that resist direct principle application.

TRIZ classifies contradictions as technical (improving parameter A worsens parameter B) or physical (a parameter must be both X and not-X simultaneously), then applies inventive principles and separation strategies to break them. For physical contradictions, four Separation Principles apply: separation in time, space, condition, or scale.

**Triggered when:** A primary lens flags explicit "we need X but X causes Y" contradictions, a design trade-off appears unresolvable within the primary framework, or optimization within existing constraints has been exhausted.
**Not needed when:** The primary lens resolved all contradictions on its own, or the issue is a bottleneck, risk exposure, or ambiguity rather than a trade-off.

---

### 6. Antifragile (Taleb)

**Skill:** `/seal-strategy-antifragile`
**Framework:** Taleb's Antifragile: the triad, barbell strategy, via negativa, optionality
**Best for:** Problems involving concentration risk, fragility, optimization at the expense of resilience, or systems with no margin for error.

The key distinction: fragile things break under stress, robust things resist stress, **antifragile things get stronger from stress.** The goal isn't just survival. It's designing systems that benefit from volatility.

The lens assesses every finding on the Fragile/Robust/Antifragile triad, maps concentration (single points of failure in revenue, people, channels, suppliers), checks for Black Swan exposure, identifies iatrogenics (interventions causing more harm than the problem), and defaults to Via Negativa: improving by removing fragilities, dependencies, and complexity rather than adding.

**Use when:** Revenue or operations are concentrated in few clients/channels, the business has no margin for error, growth has come at the cost of resilience, or there's been a recent shock or near-miss.
**Don't use when:** The problem is a clear bottleneck (use TOC), the problem is operational inefficiency (use Default), or you need to resolve specific contradictions (use TRIZ).

---

### 7. Wardley Mapping (Wardley)

**Skill:** `/seal-strategy-wardley`
**Framework:** Simon Wardley's value chain evolution mapping
**Best for:** Problems where the business is investing heavily in activities that don't match their evolutionary stage. Custom-building commodity, outsourcing genesis, treating everything the same.

Wardley Mapping anchors on the user need, maps every component in the value chain, and classifies each by evolutionary stage: Genesis (novel, uncertain) → Custom-Built (understood but not standardized) → Product (standardized, feature competition) → Commodity (price competition, "just works"). Everything evolves left to right. This is not optional.

The strategic value comes from finding mismatches: components managed at the wrong evolutionary stage. A business custom-building its CRM when off-the-shelf products exist. A business outsourcing the one activity that actually differentiates it. A business investing in incremental improvements to something that's about to be commoditized.

**Use when:** It's unclear where the business actually creates unique value, technology or process choices seem outdated or premature, or the business is investing heavily in activities competitors all do the same way.
**Don't use when:** The problem is a throughput bottleneck (use TOC), the problem is ambiguity about what kind of problem it is (use Cynefin), or the business is small and simple with few components.

---

### 8. Root Cause (Toyota 5 Whys / Ishikawa), Post-Lens Specialist

**Skill:** `/seal-rootcause`
**Framework:** 5 Whys, Ishikawa (Fishbone) Diagrams, Fault Tree Analysis, Convergence Analysis
**Role:** Post-lens specialist. Takes unexplained symptoms flagged by a primary lens and drills into their causes. Not a peer lens; it doesn't analyze the full findings.

Root Cause activates when a primary lens encounters symptoms it can explain *that* something is happening but not *why*. Its input is the specific flagged symptoms, not all Phase 1 findings.

For each flagged symptom, it asks "why?" repeatedly until it reaches an actionable cause, stopping when it finds something the business can fix, not when it reaches philosophy. It categorizes causes across six branches (People, Process, Technology, Policy, Environment, Measurement) and checks for convergence, where multiple 5-Why chains trace back to the same root cause.

The highest-leverage output is the convergence map: the single root cause driving multiple symptoms. Fix it, and several problems resolve simultaneously. The second most valuable output is the "what NOT to fix" list, symptoms that will resolve on their own once the root cause is addressed.

**Triggered when:** A primary lens flags symptoms it can describe but not explain, band-aid fixes keep appearing in the strategy, or multiple findings seem to share a hidden common driver.
**Not needed when:** The primary lens explained all symptoms adequately, or the issue is a contradiction, a decision, or ambiguity rather than an unexplained symptom.

---

### 9. Jobs to Be Done (Christensen / Ulwick)

**Skill:** `/seal-strategy-jtbd`
**Framework:** Christensen's JTBD Theory + Ulwick's Outcome-Driven Innovation
**Best for:** Problems where the business is operationally sound but strategically misaligned. Declining engagement despite good execution, customers using the product in unexpected ways, competitors winning on "fit" rather than features.

JTBD reframes the analysis through a single question: **what job is the customer hiring this to do?** Customers don't buy products. They hire them to make progress in specific circumstances. Every job has functional, emotional, and social dimensions. The business may be over-delivering on outcomes customers don't care about while under-delivering on the ones they do.

The lens maps the Forces of Progress (what pushes customers toward a new solution, what pulls them, what anxiety prevents switching, what habit keeps them in place), identifies overserved vs. underserved outcomes, checks for strategic misalignment between the job and the solution, and identifies non-consumption: people who should be "hiring" this but aren't because no solution fits their job.

**Use when:** Retention is declining despite good operations, customers are choosing competitors who seem inferior on features, or the business can't explain why customers choose them (or don't).
**Don't use when:** The problem is clearly operational (use Default or TOC), there's no customer-facing data in Phase 1, or the business has strong product-market fit and the problem is elsewhere.

---

### 10. Real Options, Post-Lens Specialist

**Skill:** `/seal-options`
**Framework:** Real Options Theory (adapted from financial options for business strategy)
**Role:** Post-lens specialist. Takes high-stakes decisions flagged by a primary lens and evaluates commit-vs-defer timing. Not a peer lens; it doesn't analyze the full findings.

Real Options activates when a primary lens surfaces a major decision it can frame but can't evaluate, typically irreversible commitments with unclear returns where "decide now" pressure may be premature. Its input is the specific flagged decisions, not all Phase 1 findings.

The core insight: **you don't have to decide now.** Options have value. The right to act in the future, without the obligation, is worth something. Most businesses destroy value by committing too early when they could keep options open cheaply.

For each flagged decision, it classifies reversibility and stakes, identifies whether the commitment pressure is real or manufactured, designs cheap probes that generate information before the big commitment, defines kill criteria (preventing zombie projects), and maps the decision timeline: when each option expires and what the last responsible moment is.

**Triggered when:** A primary lens flags fork-in-the-road decisions with high irreversibility and uncertain returns, "bet the company" choices, or strategic ambiguity from market shifts or technology transitions.
**Not needed when:** The primary lens resolved all decisions adequately, decisions are straightforward with low uncertainty, or speed of commitment matters more than optionality.

---

## Using SEAL in Personal Life

SEAL was designed for business audits, but its architecture (verify before you strategize, strategize before you act, separate facts from assumptions, pick the right framework for the shape of the problem) applies to any high-stakes analysis where getting it wrong is expensive.

The decision rule is the same: **use SEAL when the cost of a wrong answer > the cost of being slow.** In personal life, the highest-cost decisions are often the most under-analyzed because they feel like they should be "intuitive."

### Career Transitions

Career decisions are data-rich: salary, market rates, skills inventory, satisfaction signals, network strength, industry trajectory. But most people make career moves based on a mix of verified facts and unexamined assumptions. SEAL's Phase 1 separates what you *know* about your career situation from what you *assume*.

Phase 0 (data collection) might request: current compensation breakdown, time allocation audit, skills inventory with evidence of proficiency, network map, market rate data for target roles, satisfaction scores across dimensions (autonomy, compensation, meaning, growth, relationships).

Phase 1 (audit) would verify: what the data actually shows about your career trajectory vs. what you tell yourself. "I'm underpaid" might be a verified finding or an unverified claim depending on whether you've checked market data. "I have no options" is almost always a claim without evidence.

The lenses map cleanly to different career problem shapes:

- **Real Options.** "Should I take this offer or wait?" Real Options would inventory your decisions, classify each by reversibility, identify whether the pressure to decide is real or manufactured, and design probes (informational interviews, freelance projects, internal transfers) that generate information before irreversible commitment.
- **Jobs to Be Done.** "I have a good job but something feels off." JTBD would ask what "job" you're hiring your career to do. Most people optimize for the wrong dimension: salary when the actual job-to-be-done is autonomy, prestige when the job is meaning, stability when the job is growth. The misalignment between the job and the solution explains the dissatisfaction.
- **Theory of Constraints.** "I'm working hard but not advancing." TOC would find the ONE constraint limiting your career throughput. It's rarely "more skills" and often something like visibility, positioning, or a policy constraint (you're in a role with a ceiling).
- **Antifragile.** "What if I lose my job?" Antifragile would map your concentration risk: one employer, one industry, one geography, one income stream. It would design barbell strategies with extreme stability on one side (emergency fund, transferable skills, maintained network) and small aggressive bets on the other (side projects, new skill experiments, relationship building in adjacent industries).
- **Cynefin.** "I don't even know what kind of career problem I have." Cynefin would classify different aspects of your career situation into domains. Your technical skill gap might be Complicated (analyzable, solvable with expertise). Your industry's future might be Complex (unpredictable, needs probing). Your immediate cash flow problem might be Clear (obvious fix, just do it).

### Personal Finances

This is the closest personal analogue to a business audit. Real numbers, real data, real contradictions between spending and stated priorities.

Phase 1 forensics on personal finances almost always reveals a gap between "where I think my money goes" and "where it actually goes." The audit would inventory income sources, categorize spending, identify trends, flag contradictions (says saving is a priority but savings rate is 3%), and separate verified financial position from assumptions ("I can afford this" based on what data?).

The Default lens works well here for clear findings that need prioritization. But Antifragile often reveals deeper issues: income concentrated in one source, no buffer for shocks, lifestyle scaled to maximum income with no margin. TOC might find that the constraint isn't income but a single recurring expense category consuming disproportionate resources.

### Major Life Decisions

Buying property, relocating, getting married, having children, retiring. These are high-stakes, mostly irreversible, and benefit enormously from separating verified facts from emotional assumptions before committing.

**Real Options is the most powerful lens here.** Most people commit to major life decisions too early because the pressure to decide *feels* urgent when it often isn't. Real Options would ask: What's the last responsible moment for this decision? What's the cost of waiting vs. the cost of committing? What cheap probes could generate more information before you lock in? What kill criteria would tell you to walk away?

Example: Buying a house. Phase 1 would audit the actual financial data (not what the mortgage broker says you can afford, but what the data shows you can sustain). Real Options would identify: Can you rent in the target area first? (Probe.) What market conditions would make you walk away? (Kill criteria.) Is the "act now or miss out" pressure real or manufactured? (Expiration analysis.) What flexibility do you lose by buying? (Irreversibility classification.)

### Health Optimization

Wearable data, bloodwork, training logs, sleep patterns, nutrition tracking. Modern health is increasingly data-rich. Phase 1 can audit what the data actually shows vs. what you believe about your health.

**Root Cause** works well here. "Why am I always tired?" has a 5-Whys chain that usually ends somewhere surprising. Surface answer: not enough sleep. Why? Working late. Why? Behind on projects. Why? Overcommitted. Why? Can't say no. Root cause: a boundary-setting problem, not a sleep problem. Fixing the sleep hygiene without fixing the root cause is a band-aid.

**Systems Thinking** catches the loops that Root Cause might miss. "I'm stressed so I don't exercise, so I sleep poorly, so I'm less productive, so I work longer, so I'm more stressed" is a reinforcing loop. Intervening at any point in the loop can break it, but some intervention points are higher leverage than others. Systems Thinking finds those.

**TOC** can identify the single constraint limiting health outcomes. If you're trying to lose weight, get stronger, sleep better, reduce stress, and eat cleaner simultaneously, TOC would ask: which ONE of these, if improved, would have the biggest cascade effect on the others? Improve that one. Subordinate everything else to it.

### Recurring Personal Patterns

"Why does this keep happening to me?" is a systems question. SEAL's Phase 1 would audit the pattern forensically: when does it happen, what preceded it, what data do you actually have vs. what narrative have you constructed? Phase 2 through Systems Thinking or Root Cause would dig into the structure.

The system archetypes map directly to personal patterns:

- **Shifting the Burden.** Using short-term coping (alcohol, spending, avoidance) instead of addressing the underlying issue. The coping mechanism weakens your ability to address the real problem, increasing dependence on the coping mechanism.
- **Eroding Goals.** Gradually accepting lower standards. "I used to run 3x/week, then 2x, then occasionally, then never." Each small concession feels reasonable; the cumulative drift is invisible until you audit it.
- **Fixes That Fail.** Solving today's stress by creating tomorrow's problem. Taking on debt to relieve financial anxiety. Saying yes to avoid conflict, creating a larger conflict later.
- **Success to the Successful.** One area of life gets all the investment while others starve. Career success funded by relationship neglect. Health optimization at the cost of social connection.
- **Limits to Growth.** A strategy that worked brilliantly hits a ceiling. The hustle that built your career now prevents its next phase. The frugality that built savings now prevents experiences.

### Time Audits

Where does your time actually go? Phase 1 forensics against calendar data, screen time reports, and self-reported "how I spend my day" almost always reveals a significant gap.

**Wardley Mapping** applies here in a way it rarely does to personal life elsewhere. Classify every recurring time expenditure by its "evolutionary stage." Is this something that requires your unique judgment and creativity (genesis), or is it routine and could be automated, delegated, or eliminated (commodity)? Most people spend enormous personal energy on commodity activities (grocery shopping, bill paying, routine communications) managed as if they were custom, while starving the genesis activities that actually move their life forward.

### When SEAL Doesn't Fit Personal Life

- **Emotional decisions that aren't actually decisions.** "Should I forgive this person?" is not a data problem. There's nothing for Phase 1 to verify.
- **Day-to-day choices.** What to eat, what to watch, what to do this weekend. The overhead isn't justified.
- **Anything where intuition is the signal.** Relationships, creative work, spiritual practice. The data is internal, not auditable.
- **Urgent situations.** Health emergencies, immediate safety. Act first, analyze later. (Cynefin's Chaotic domain says exactly this: in chaos, any action to stabilize is better than analysis.)
- **Low-stakes decisions.** If the cost of getting it wrong is trivial, SEAL's thoroughness is wasted overhead.

### Personal Life Lens Quick Reference

| Life problem shape                                            | Best lens                                        |
| ------------------------------------------------------------- | ------------------------------------------------ |
| "I need to make a big decision but I'm uncertain"             | Real Options (post-lens specialist)              |
| "Things are fine on paper but something feels off"            | Jobs to Be Done                                  |
| "I'm stuck and don't know why"                                | Theory of Constraints                            |
| "I keep ending up in the same place despite trying to change" | Systems Thinking or Root Cause (post-lens specialist) |
| "One bad event could wreck everything"                        | Antifragile                                      |
| "I'm busy all the time but not making progress"               | Wardley Mapping                                  |
| "I don't even know what kind of problem this is"              | Cynefin                                          |
| "I know what to do, just need to prioritize"                  | Default                                          |
| "I want X but getting X prevents Y"                           | TRIZ (post-lens specialist)                      |

---

## The Complete System

| Skill | Role |
|-------|------|
| `/seal-run` | Orchestrator: chains all phases, enforces gates |
| `/seal-collect` | Phase 0: Data Collector |
| `/seal-audit` | Phase 1: Forensic Auditor + Pareto Map |
| `/seal-review` | Critic: runs after every phase including specialists |
| `/seal-strategy-lens` | Lens Selector: Cynefin-based classification + specialist pre-scan |
| **Primary Lenses (Phase 2)** | |
| `/seal-strategy` | Default (Impact/Effort) |
| `/seal-strategy-toc` | Theory of Constraints |
| `/seal-strategy-wardley` | Wardley Mapping |
| `/seal-strategy-antifragile` | Antifragile |
| `/seal-strategy-systems` | Systems Thinking |
| `/seal-strategy-jtbd` | Jobs to Be Done |
| **Post-Lens Specialists (Phase 2b)** | |
| `/seal-triz` | TRIZ: resolves contradictions |
| `/seal-rootcause` | Root Cause: drills into symptoms |
| `/seal-options` | Real Options: evaluates decisions |
| **Drafting** | |
| `/seal-draft` | Phase 3: Operational docs + copy briefs |
