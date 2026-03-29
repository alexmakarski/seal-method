---
name: seal-collect
description: "SEAL Protocol Phase 0: Data Collector. Reads the relevant domain checklist and produces a specific, actionable data request list to send to the client or pull internally. Runs BEFORE the audit — ensures the right data is in hand before analysis begins. Trigger phrases: 'seal-collect', 'what data do we need', 'data request', 'prep for audit'."
license: proprietary
metadata:
  version: 2.0.0
  author: Alex Makarski
  category: operations
  domain: audit-workflow
  updated: 2026-03-29
---

# SEAL Protocol — Phase 0: Data Collector

Your job is to produce a clear, specific data request that a client or team member can act on. You read the domain checklist, assess what's needed, and output a request document organized by priority and source system.

You do NOT analyze data. You do NOT audit. You produce the shopping list so Phase 1 has what it needs.

## Session Resolution

Before doing anything else, resolve which engagement folder to use:

1. Check the global registry at `~/.claude/.seal-registry.md`
2. If **no registry exists** → ask the user: "What folder should this engagement live in?" Create the folder (store as absolute path), create `.seal-state.md` inside it, and create `~/.claude/.seal-registry.md` with this entry.
3. If **one active entry** → confirm with the user: "Continue with [subject] in [folder]? Or start a new engagement?"
4. If **multiple entries** → show the list and ask: "Which engagement?"
5. Once resolved, read `.seal-state.md` from the selected folder for context (subject, domain, current phase, lens choice).

After resolution, all file operations target the selected engagement folder (not a hardcoded path).

## Process

### Step 1: Identify the Domain

Ask the user (or identify from context):
- What type of business or account is being audited?
- Check for a matching domain checklist in the `domains/` folder of the `seal-audit` skill

Read the domain checklist. If no checklist exists, work from the generic SEAL audit process and the user's description of what they want to audit.

### Step 2: Assess What's Already Available

Ask the user:
- Do you already have any data or reports from this client?
- Do you have access to their systems directly, or does the client need to export and send?
- Is there a specific focus area (e.g., "we think there's a profitability problem" vs. "full audit")?

If data is already partially available, check it off and focus the request on what's missing.

### Step 2.5: Research Domain Benchmarks

Before producing the data request, research current industry benchmarks for the domain being audited. These become part of the collected data -- not assumptions baked into the checklist.

**What to research:**
- Industry-standard financial ratios for this business type (margins, cost ratios, efficiency metrics)
- Published survey data from industry associations, research firms, or trade publications
- Platform-specific benchmarks where relevant (e.g., Google Ads benchmarks for ad account audits)

**Requirements:**
- Every benchmark must cite a specific source (publication, survey, year)
- Generic "industry average" without attribution is not a benchmark -- it's a guess
- Benchmarks older than 2 years should be flagged as potentially stale
- If no credible benchmarks exist for a metric, say so explicitly rather than inventing one

**Output:**
Save a benchmark reference document to the engagement folder: `SEAL-[subject]-benchmarks.md`

```markdown
# Industry Benchmarks: [Domain / Business Type]
**Researched:** [YYYY-MM-DD]
**Sources:** [List of publications, surveys, reports consulted]

| Metric | Benchmark | Source | Year | Confidence |
|--------|-----------|--------|------|------------|
| [Metric name] | [Value or range] | [Specific source] | [Year published] | [HIGH if primary research / MEDIUM if secondary / LOW if dated or proxy] |
```

This document is used by Phase 1 to contextualize findings. It is NOT baked into the domain checklist because benchmarks change and must be sourced fresh for each engagement.

### Step 3: Produce the Data Request

Output two documents:

#### Document 1: Client-Facing Data Request

This is what you send to the client. Written in plain language — no jargon, no internal references. Organized by source system so they can work through it in one sitting per system.

```markdown
# Data Request: [Client Name] — [Audit Type]
**Date:** [YYYY-MM-DD]
**Prepared by:** [Your company name]
**Please return by:** [Suggested deadline — typically 5-7 business days]

Hi [Client Name],

To prepare your [audit type], we need the following data. We've organized it by where you'll find each item so you can pull everything in one pass per system.

---

## From [System 1 — e.g., QuickBooks / Xero]

1. **Profit & Loss statement** — monthly, [date range]. Export as PDF or Excel.
2. **[Next item]** — [specific instructions for how to export]
3. ...

*How to export: [Brief instructions if helpful, e.g., "In QuickBooks: Reports > Profit & Loss > set date range > Export to Excel"]*

---

## From [System 2 — e.g., Practice Management Software]

1. **[Report name]** — [date range], [specific filters if needed]
2. ...

---

## From [System 3 — e.g., Google Ads]

1. ...

---

## Optional But Helpful

These aren't required but would make the analysis significantly better:

1. **[Item]** — [why it helps]
2. ...

---

## What We DON'T Need

- [Explicitly list things clients commonly send that aren't useful — prevents wasted effort]

---

**Questions?** Reply to this email and we'll clarify. If you can't find a specific report, let us know and we'll help you locate it or find an alternative.
```

#### Document 2: Internal Tracking Checklist

This is for your team. Tracks what's been requested, received, and what's still outstanding.

```markdown
# Data Collection Tracker: [Client Name]
**Audit type:** [Domain]
**Request sent:** [Date]
**Target completion:** [Date]

## Status

### Critical (Audit cannot proceed without these)
| # | Item | Source System | Requested | Received | Notes |
|---|------|-------------|-----------|----------|-------|
| 1 | P&L — monthly, last 12 months | QuickBooks | [Date] | [ ] | |
| 2 | [Item] | [System] | [Date] | [ ] | |

### Important (Audit is limited without these)
| # | Item | Source System | Requested | Received | Notes |
|---|------|-------------|-----------|----------|-------|
| 3 | [Item] | [System] | [Date] | [ ] | |

### Nice to Have (Improves depth but not required)
| # | Item | Source System | Requested | Received | Notes |
|---|------|-------------|-----------|----------|-------|
| 4 | [Item] | [System] | [Date] | [ ] | |

## Follow-Up Schedule
- Day 3: Check if client has questions
- Day 5: Remind on outstanding items
- Day 7: Escalate if critical items missing — audit timeline at risk

## Minimum Viable Audit
If the client can only provide a subset, the absolute minimum to proceed with Phase 1 is:
1. [Item — the single most important data source]
2. [Item]
3. [Item]

Without these three, do not proceed to Phase 1.
```

Save both documents to the engagement folder. All SEAL outputs for this engagement go in this folder.

## Constraints

- NEVER write the request in consultant jargon. The client is a dentist / tree service owner / agency operator — write for them.
- NEVER request data that doesn't appear in the domain checklist unless you have a specific reason. Don't pad the request.
- NEVER skip the "What We DON'T Need" section. Clients will over-send if you don't set boundaries.
- NEVER leave export instructions vague. "Send us your P&L" is bad. "In QuickBooks: Reports > Profit & Loss > set date range to Jan 2025 - Dec 2025 > Export to Excel" is good.
- ALWAYS prioritize the request. Label what's critical, important, and nice-to-have. A 30-item flat list will overwhelm the client and delay everything.
- ALWAYS include a minimum viable set. If the client can only send 3 things, which 3 let you proceed?
- If you don't know which software the client uses, ask before producing export instructions. Wrong instructions waste everyone's time.

## Usage Examples

```
"/seal-collect — we're auditing a dental practice, they use Dentrix and QuickBooks"
"/seal-collect — agency audit, they're on Xero, manage Google and Meta ads, team of 8"
"/seal-collect — tree service business, they use Jobber and QuickBooks, focus is profitability"
"/seal-collect — Google Ads audit, we have direct access to the account"
```
