# SEAL Domain Checklist: Agency (Media Buying / Analytics / Digital Marketing)

Use this checklist alongside `/seal-audit` when auditing a media buying, analytics, or digital marketing agency.

---

## Data Sources to Inventory

### Financial / Accounting (QuickBooks, Xero, CPA reports)
- [ ] P&L — monthly, last 12 months minimum
- [ ] Revenue by client — who pays what, monthly
- [ ] Revenue by service type — media management, analytics/reporting, strategy, creative, one-time projects
- [ ] Client retainer schedule — contracted monthly amounts vs. actual collected
- [ ] Accounts receivable aging — who owes what and how old
- [ ] Media spend managed — total ad spend under management (not agency revenue)
- [ ] Payroll / contractor detail — who costs what, billable vs. non-billable roles
- [ ] Software/tool costs — ad platforms, analytics tools, reporting tools, project management, AI tools
- [ ] Client acquisition cost — sales cycle spend, pitch costs, free audits given

### Client Portfolio
- [ ] Client roster — name, start date, monthly retainer, services provided, contract terms
- [ ] Client tenure — how long each client has been active
- [ ] Client churn history — who left, when, why (if tracked)
- [ ] Client concentration — revenue distribution across clients
- [ ] Contract terms — notice periods, scope definitions, rate escalation clauses
- [ ] Scope creep log — if maintained (work done outside contract scope)

### Team / Operations
- [ ] Org chart / team roster — roles, tenure, compensation, billable vs. overhead
- [ ] Client-to-team ratio — how many clients per account manager / media buyer
- [ ] Time tracking data — if used (billable hours by client, by team member)
- [ ] Utilization rates — billable hours ÷ available hours per team member
- [ ] Freelancer/contractor roster — who, for what, rates, reliability
- [ ] SOPs / documented processes — what's documented vs. tribal knowledge

### Delivery / Performance
- [ ] Client reporting cadence — weekly, monthly, quarterly? Consistent?
- [ ] Client KPIs — what's being measured per client, who set the targets
- [ ] Media spend efficiency — ROAS, CPA, CPL by client (what clients are actually getting)
- [ ] Platform certifications — Google Partner, Meta Partner, etc.
- [ ] Case studies / results documentation — proof of outcomes

### Sales / Pipeline
- [ ] Pipeline / CRM data — leads, proposals, close rate
- [ ] Average deal size — new client retainer value
- [ ] Sales cycle length — time from first contact to signed contract
- [ ] Proposal win/loss log — if tracked
- [ ] Lead sources — referral, inbound, outbound, partnerships
- [ ] Churn rate vs. new client acquisition rate — net growth or net shrinkage

### Client Satisfaction
- [ ] NPS or satisfaction scores — if measured
- [ ] Client feedback / survey results — if collected
- [ ] Testimonials / case studies — what clients say publicly
- [ ] Escalation / complaint history — if tracked
- [ ] Client meeting notes — sentiment indicators

---

## Metrics to Extract

### Financial Health
| Metric | What to Extract | Benchmark Range |
|--------|----------------|-----------------|
| Annual revenue | Total agency revenue (not media spend) | Context-dependent |
| Revenue per employee | Agency revenue ÷ FTE count | $150,000-250,000+ |
| Gross margin | (Revenue - direct delivery costs) ÷ Revenue | 50-70% |
| Net profit margin | Net income ÷ Revenue | 15-25% |
| Effective hourly rate | Revenue ÷ Total billable hours delivered | $100-250+ depending on market |
| Payroll ratio | Total people cost ÷ Revenue | 45-55% |
| Tool/software cost ratio | All tools ÷ Revenue | 5-10% |
| Client acquisition cost | Sales + marketing cost ÷ New clients won | Context-dependent |
| Revenue per client | Average monthly retainer × 12 | Context-dependent |

### Client Portfolio Health
| Metric | What to Extract | Benchmark Range |
|--------|----------------|-----------------|
| Client count | Total active clients | Context-dependent |
| Client concentration | Top client as % of revenue | Under 20% for any single client |
| Top 3 concentration | Top 3 clients as % of revenue | Under 40% |
| Average client tenure | Mean months of active clients | 12+ months is healthy |
| Monthly churn rate | Clients lost ÷ Total clients (monthly) | Under 3% monthly / 25% annual |
| Net revenue retention | (Revenue from existing clients this year) ÷ (Revenue from same clients last year) | 100%+ means growing within accounts |
| Average retainer value | Mean monthly retainer across clients | Context-dependent |
| Retainer distribution | How many clients at each price tier | Healthy = pyramid, not barbell |

### Team Efficiency
| Metric | What to Extract | Benchmark Range |
|--------|----------------|-----------------|
| Clients per account manager | Client count ÷ AM headcount | 5-10 depending on complexity |
| Clients per media buyer | Client count ÷ Buyer headcount | 5-8 depending on spend level |
| Utilization rate | Billable hours ÷ Available hours | 70-80% |
| Delivery cost per client | Direct labor + tools for client ÷ Retainer | Under 60% of retainer |
| Employee tenure | Average months of employment | 18+ months is healthy |
| Turnover rate | Employees who left ÷ Average headcount (annual) | Under 20% |

### Sales Pipeline
| Metric | What to Extract | Benchmark Range |
|--------|----------------|-----------------|
| Proposals per month | New proposals sent | Context-dependent |
| Close rate | Proposals won ÷ Proposals sent | 25-40% |
| Average sales cycle | Days from first contact to signed | 30-90 days |
| Pipeline value | Total $ of active proposals | 3x+ monthly revenue target |
| Lead-to-proposal rate | Proposals ÷ Inbound leads | Context-dependent |
| New client revenue vs. churn | Monthly new revenue added vs. lost | Positive = growing |

### Media Management (if applicable)
| Metric | What to Extract | Benchmark Range |
|--------|----------------|-----------------|
| Total media spend managed | Sum of all client ad spend | Context-dependent |
| Management fee as % of spend | Agency fee ÷ Media spend managed | 10-20% (declining with scale) |
| Revenue per dollar managed | Agency revenue ÷ Total spend managed | Context-dependent |
| Client ROAS distribution | How many clients are above/below target | Context-dependent |
| Underperforming accounts | Clients consistently below KPI targets | Flag count and duration |

---

## Contradictions to Check

### Financial
- **Revenue growth but margin compression** — Adding clients but profit isn't growing proportionally. Check: are new clients at lower retainers? Is scope creeping without rate increases? Is headcount growing faster than revenue?
- **High utilization but low profit** — Team is busy but money isn't there. Check: effective hourly rate may be too low, or too much time on non-billable work (pitches, internal, scope creep)
- **"We're profitable" vs. owner compensation** — Is the owner paying themselves a market-rate salary? Or is "profit" actually their unpaid labor? Add a fair market salary for the owner and recalculate
- **Retainer collected vs. retainer contracted** — Are clients actually paying what they agreed to? Late payments, disputed invoices, and "we'll catch up next month" erode real revenue
- **Tool costs seem low** — Are team members using personal accounts? Are there shadow subscriptions? Is the agency on free tiers that limit capability?

### Client Portfolio
- **"We have 20 clients" vs. revenue concentration** — 20 clients where 3 account for 60% of revenue is really a 3-client agency with 17 side projects
- **"Our clients love us" vs. churn data** — What's the actual retention rate? How many clients from 2 years ago are still active?
- **"We don't lose clients on performance" vs. actual results** — Are client KPIs being met? If not tracked, this claim is unverifiable
- **Long client tenure but flat retainers** — Clients staying for 3+ years at the same rate while the agency's costs increase = margin erosion per client over time
- **Scope creep as "good service"** — Agency delivers 30% more work than contracted because "we want to keep them happy." This is unpriced labor. Quantify it

### Team
- **"Our team is maxed" vs. utilization data** — Are they maxed on client work or on internal meetings, reporting overhead, and context-switching?
- **Low turnover claimed vs. actual** — Check tenure data. "People stay" means different things if average tenure is 3 years vs. 8 months
- **"We need to hire" vs. process efficiency** — Is the bottleneck headcount, or is it that each client requires manual reporting that could be automated? Would better SOPs free up 20% of current capacity?
- **Senior people doing junior work** — Is the $150/hour strategist pulling reports and building spreadsheets? Check time allocation by role vs. task type

### Sales
- **"Referrals are our main growth channel" vs. growth rate** — Referrals are great but don't scale predictably. Is the agency actually growing, or just replacing churn?
- **"We win on relationships" vs. proposal data** — What's the actual close rate? What's the common reason for losses? Is it really relationships or is it pricing, case studies, or pitch quality?
- **High proposal volume but low close rate** — Spending significant time on pitches that don't convert. What's the cost per proposal? Are they qualifying leads before investing in proposals?
- **"We don't do free work to win clients" vs. reality** — Free audits, spec work, and "discovery sessions" are free work. Quantify the investment per pitch

### Pricing
- **Percentage of spend model vs. actual work required** — A client spending $10K/month and a client spending $100K/month may require similar management hours. Is the pricing model aligned with actual delivery cost?
- **"Our rates are competitive" vs. effective hourly rate** — Calculate actual revenue ÷ actual hours delivered per client. Many agencies discover their effective rate is $50-75/hour when they think they're charging $150+
- **Flat retainer vs. growing scope** — Original scope was 2 platforms, now it's 4 plus reporting plus creative feedback. Has the retainer adjusted?

---

## Common Claims Without Evidence

| Common Claim | What Data Would Verify It |
|-------------|--------------------------|
| "We manage $X million in ad spend" | Actual platform spend reports summed across all clients — not projected or annualized from best month |
| "Our average client ROAS is 4x" | ROAS by client — is this the average or the best client? What about the ones below target? |
| "We have a 90% retention rate" | Annual churn calculation — clients lost ÷ starting client count. Month-to-month, or including clients who stayed 2 months? |
| "We're at capacity" | Utilization data — billable hours vs. available. "Feels busy" is not a metric |
| "Our team is our competitive advantage" | Employee tenure, client satisfaction scores, and whether clients follow people who leave |
| "We don't compete on price" | Win/loss data — why are proposals actually lost? |
| "Revenue is growing" | Monthly revenue trend — is it actually growing net of churn, or just replacing lost clients? |
| "We're diversified across industries" | Revenue by client industry — diversity in client count doesn't matter if 70% of revenue is one vertical |
| "We add value beyond media buying" | Scope of work vs. what clients actually use/engage with. Strategic decks that go unread aren't "value" |
| "We could grow faster if we hired" | Pipeline data + close rate + current utilization. Is the bottleneck delivery capacity or sales volume? |

---

## Agency Business Model Analysis

When enough data is available, classify the agency model and flag structural risks:

### Revenue Model
| Model | What to Check | Risk |
|-------|--------------|------|
| % of spend | Fee scales with client budget | Revenue drops when clients cut spend — you eat their downturn |
| Flat retainer | Fixed monthly fee per client | Scope creep erodes margin; must renegotiate annually |
| Project-based | One-time fees for audits, builds, launches | No recurring revenue; feast/famine cash flow |
| Performance-based | Fee tied to results | Misaligned incentives, harder to forecast, dispute-prone |
| Hybrid | Mix of the above | Complexity in tracking — make sure each component is actually profitable |

### Structural Risks to Flag
- **Single-channel dependency** — If 80%+ of delivery is one platform (Meta, Google), platform changes are an existential risk
- **Key person dependency** — If one person holds all the client relationships or all the technical knowledge, they are the real business
- **No documented processes** — Everything is in people's heads. Every new hire starts from zero. Every departure is a crisis
- **Referral-only growth** — Healthy but not scalable or predictable. One bad quarter with no new referrals = cash crunch
- **Below-market pricing with premium positioning** — Agency brands itself as strategic/premium but charges less than competitors. The positioning and pricing must match
- **Media spend concentration** — If one client represents 40%+ of managed spend, losing that client restructures the entire agency

---

## What This Checklist Does NOT Cover

- Specific platform audit methodology (Google Ads, Meta Ads, etc.) — use the `google-ads.md` checklist for that
- Creative quality assessment
- Individual campaign strategy evaluation
- Legal review of client contracts (though contract terms are in scope as business data)
- Tax planning or entity structure optimization
- Detailed HR compliance (though staffing costs and turnover are in scope)
