# SEAL Method

**Strategic Evidence Authority Ladder**

SEAL is a multi-phase audit method for Claude Code that finds the vital few things that matter in any complex situation (the 80/20 of whatever outcome you care about) and backs them with verified evidence, not opinions.

Feed it messy data. It finds everything. Then it ranks findings by impact on whatever outcome you defined, draws the 80/20 line, and tells you which 3-5 things account for most of your upside. With citations, not guesses.

## How it works

```
Phase 0: Data Collection
Phase 1: Forensic Audit + Pareto Map (80/20 ranking)
Phase 2: Strategic Analysis (6 lenses: TOC, Wardley, Antifragile, Systems, JTBD, Default)
Phase 3: Operational Deliverables + Copy Briefs
```

Every phase is role-locked. The auditor can't recommend. The strategist can't invent findings. The drafter can't change priorities. An automated critic reviews each phase before a human gate lets the next one proceed.

## What's inside

- **15 skills** that install into Claude Code
- **8 domain checklists** (dental, Google Ads, tree service, agency, tax, marketing data, professional services, membership community)
- **6 strategic lenses** so the same data gets analyzed through the right framework for the problem shape
- **3 post-lens specialists** (TRIZ for contradictions, Root Cause for unexplained symptoms, Real Options for high-stakes decisions)

## Install

```bash
./install-seal.sh
```

Or see [INSTALL.md](INSTALL.md) for details.

## Quick start

Open Claude Code in any project directory and run:

```
/seal-run
```

The orchestrator walks you through intake, data collection, audit, strategy, and deliverables. For a lighter touch, run just the audit:

```
/seal-audit
```

This gives you the forensic audit with Pareto Map. No strategy, no deliverables. Just the findings and the 80/20.

## The Pareto Map

Every SEAL engagement starts with one question: **"What does winning look like?"**

The answer becomes the axis everything gets ranked against. Revenue, time, health, speed. The Pareto Map estimates each finding's impact on that outcome, ranks them all, and draws a line. Above the line: the vital few. Below: noise.

## Read more

[SEAL-Method.md](SEAL-Method.md) is the full methodology document covering the architecture, all 10 strategic lenses and specialists, failure modes SEAL prevents, and applications to personal life.

## Requirements

- [Claude Code](https://claude.ai/claude-code) (Anthropic's CLI)
- Claude Max or Team subscription
- macOS or Linux (Windows: use WSL)

## License

MIT — see [LICENSE](LICENSE).
