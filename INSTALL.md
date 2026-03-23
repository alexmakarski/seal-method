# Installing SEAL Protocol

## Prerequisites

1. **Claude Code** (Anthropic's CLI) installed and working
2. An active Claude Max or Team subscription
3. macOS or Linux (Windows users: use WSL)

## Quick Install (30 seconds)

1. Download this entire SEAL folder to your computer
2. Open Terminal
3. Run:

```bash
cd /path/to/SEAL
./install-seal.sh
```

That's it. The script copies all 15 SEAL skills into `~/.claude/skills/`.

## Manual Install

If the script doesn't work, copy each folder from `skills/` into `~/.claude/skills/`:

```bash
cp -r skills/seal-* ~/.claude/skills/
```

## Verify It Works

Open Claude Code in any project and type:

```
/seal-run
```

You should see the SEAL orchestrator ask for intake information. If you see "skill not found," the skills weren't copied to the right location.

## What Gets Installed

| Skill | What It Does |
|-------|-------------|
| `seal-run` | Orchestrator — chains all phases, enforces quality gates |
| `seal-collect` | Phase 0 — produces data request for client |
| `seal-audit` | Phase 1 — forensic audit with Pareto Map |
| `seal-review` | Critic — runs after every phase automatically |
| `seal-strategy-lens` | Lens selector — routes to the right strategic framework |
| `seal-strategy` | Default lens (Impact/Effort prioritization) |
| `seal-strategy-toc` | Theory of Constraints lens |
| `seal-strategy-wardley` | Wardley Mapping lens |
| `seal-strategy-antifragile` | Antifragile lens |
| `seal-strategy-systems` | Systems Thinking lens |
| `seal-strategy-jtbd` | Jobs to Be Done lens |
| `seal-triz` | Post-lens specialist — contradiction resolution |
| `seal-rootcause` | Post-lens specialist — root cause analysis |
| `seal-options` | Post-lens specialist — real options evaluation |
| `seal-draft` | Phase 3 — produces deliverables and copy briefs |

## Domain Checklists (included)

Inside `seal-audit/domains/` you'll find sector-specific checklists:

- Dental practice
- Google Ads / GA4
- Tree service / arborist
- Agency (media buying / digital marketing)
- Tax discovery
- Marketing data readiness
- Professional services
- Membership community

These guide the audit with industry-specific data inventories, benchmarks, and common contradiction patterns.

## How to Use

### Full engagement (all phases):
```
/seal-run
```
Follow the prompts. The orchestrator will walk you through intake, data collection, audit, strategy, and deliverables — with quality reviews and approval gates between each phase.

### Quick Pareto Scan (Phase 0 + 1 only):
```
/seal-collect
```
Then when data arrives:
```
/seal-audit
```
This gives you the forensic audit with Pareto Map — the "vital few" findings ranked by impact on the desired outcome. No strategy, no deliverables. Hand the Pareto Map to the client and have the conversation.

### Individual phases:
Any skill can be run standalone. Use `/seal-audit` for just the audit, `/seal-strategy-toc` for just a TOC analysis on existing findings, etc.

## Updating

When a new version is released, just run `./install-seal.sh` again. It will overwrite the existing skills.

## Troubleshooting

**"Command not found" when running the installer:**
```bash
bash install-seal.sh
```

**Skills don't appear in Claude Code:**
Check that the files landed in the right place:
```bash
ls ~/.claude/skills/seal-*
```
You should see 15 directories.

**Claude Code says "skill not found":**
Restart Claude Code after installing. Some versions cache the skill list on startup.
