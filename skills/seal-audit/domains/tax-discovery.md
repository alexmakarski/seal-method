# SEAL Domain Checklist: Tax Discovery

Use this checklist alongside `/seal-audit` when performing tax discovery for an individual or small business. This defines what data to look for, what to extract, and what contradictions to check.

This is a **discovery and planning** checklist — not a return preparation checklist. The goal is to identify what's being done, what's being missed, and where the money is.

---

## Data Sanitization Protocol

Before submitting ANY tax data to an LLM, strip all personally identifiable information and replace with variables.

| Data Type | Variable Format | Example |
|-----------|----------------|---------|
| Individual names | USP1, USP2 | "John Smith" → USP1 |
| Entity names | ENT1, ENT2 | "Smith Holdings LLC" → ENT1 |
| SSN/EIN | [REDACTED-SSN-1], [REDACTED-EIN-1] | Never submitted, not even as variables |
| Addresses | ADDR1, ADDR2 | Use state only if state matters for nexus analysis |
| Account numbers | ACCT1, ACCT2 | Bank, brokerage, retirement accounts |
| Employer names | EMP1, EMP2 | Unless the employer is public info relevant to the analysis |

Maintain a **Variable Mapping Table** in the engagement folder (`SEAL-[subject]-variable-map.md`). This file is NEVER submitted to the LLM.

---

## Source Reliability Classification: Tax Authority Ladder

This overrides SEAL's generic 3-tier source classification for tax engagements. All findings must cite their authority tier.

| Tier | Authority Type | Weight | Examples |
|------|---------------|--------|----------|
| **1** | Statutory law | Binding — highest authority | Internal Revenue Code (Title 26), ERISA, state tax statutes |
| **2A** | Supreme Court precedent + Final/Temporary Regulations | Binding — interprets statute | Treasury Regulations (26 CFR), SCOTUS tax decisions |
| **2B** | Published IRS guidance | Authoritative but not binding on courts | Revenue Rulings, Revenue Procedures, Notices, Announcements |
| **3** | IRS administrative guidance | Informational — IRS position only | Chief Counsel Advice, Field Service Advice, IRS Publications |
| **4** | Judicial authority (lower courts) | Persuasive — varies by circuit | Tax Court, District Court, Circuit Court opinions |
| **5** | Non-precedential guidance | Reference only — cannot be cited as authority | Private Letter Rulings, Technical Advice Memoranda, Practice Units |
| **6** | Secondary sources | Practitioner judgment | Treatises, journals, CPA websites, tax prep software guidance |

### Confidence Level Rules

- **HIGH confidence** findings require Tier 1 or 2A citation
- **MEDIUM confidence** findings require Tier 2B or 3 citation, corroborated by at least one other source
- **LOW confidence** findings may cite Tier 4-6 but must be explicitly flagged as non-authoritative
- Any finding citing only Tier 5-6 authority is classified as a CLAIM, not a VERIFIED FINDING

### Automatic Downgrade Rule

If a finding's cited authority fails the Citation Audit Protocol (below), it is automatically reclassified from VERIFIED FINDING to CLAIM WITHOUT EVIDENCE — regardless of how correct the conclusion appears. A right answer with a wrong citation is an unsupported position.

---

## Citation Audit Protocol

Every citation in a tax discovery must pass ALL five checks. Failure on any check triggers the automatic downgrade.

1. **Existence check** — Does the cited IRC section, regulation, revenue ruling, or case actually exist? AI frequently fabricates plausible-sounding citations.

2. **Pinpoint check** — Is the specific subsection, paragraph, or subparagraph correct and relevant to the conclusion? Getting the right code section but the wrong paragraph means the reasoning doesn't follow from the cited authority.

3. **Temporal check** — Is the cited authority still in force? Has it been superseded, revoked, amended, or sunset? Revenue rulings from the 1990s may have been obsoleted by TCJA. Check effective dates.

4. **Domain check** — Is the citation from the correct regulatory title? Title 26 (IRC) vs. Title 31 (money and finance) vs. ERISA vs. state tax code. AI conflates these regularly.

5. **Placeholder prohibition** — No citations of the form "Rev. Rul. 20XX-XX" or "IRC Sec. XXX(x)" are acceptable. If the exact citation cannot be located, state "INSUFFICIENT AUTHORITY — practitioner verification required."

---

## Data Sources to Inventory

### Prior Returns
- [ ] Federal returns — last 3 years minimum (1040, 1120/1120S, 1065, 990 as applicable)
- [ ] State returns — all filing states, last 3 years
- [ ] IRS transcripts (wage & income, account transcripts) — to cross-reference against returns
- [ ] Extension filings — any years filed late or currently on extension
- [ ] Amended returns — any 1040-X or equivalent filed
- [ ] Estimated tax payment history — quarterly payments made (1040-ES, state equivalents)
- [ ] Prior year preparer notes or organizer — if available from previous CPA/EA

### Income Documentation (Current Year + Prior)
- [ ] W-2s — all employers, all filers
- [ ] 1099-NEC / 1099-MISC — freelance, consulting, contract income
- [ ] 1099-INT / 1099-DIV — bank interest, dividends, capital gain distributions
- [ ] 1099-B — brokerage transactions (stock sales, crypto dispositions)
- [ ] 1099-R — retirement distributions, rollovers, Roth conversions
- [ ] 1099-S — real estate sale proceeds
- [ ] 1099-K — payment platform income (Stripe, PayPal, Venmo, Square, Amazon)
- [ ] K-1s — partnership, S-corp, trust, or estate distributions
- [ ] Rental income records — lease agreements, rent rolls, property management statements
- [ ] Royalty income — publishing, licensing, mineral rights
- [ ] Social Security statements (SSA-1099)
- [ ] Gambling winnings (W-2G) and loss documentation
- [ ] Foreign income — FBAR/FATCA filing requirements, foreign tax paid

### Business Records (if applicable)
- [ ] P&L statement — current year and prior, by month
- [ ] Balance sheet — current
- [ ] Business bank statements — all accounts, 12 months
- [ ] Business credit card statements — 12 months
- [ ] Payroll records — if has employees (941s, W-2s issued, state unemployment)
- [ ] 1099s issued to contractors — who was paid, was reporting done?
- [ ] Vehicle mileage log — business use percentage, total miles
- [ ] Home office documentation — square footage, total home SF, dedicated use
- [ ] Asset list / depreciation schedule — what's being depreciated, methods, remaining basis
- [ ] Entity formation documents — LLC operating agreement, S-corp election (Form 2553), EIN letter
- [ ] Reasonable compensation documentation (S-corp) — how was officer salary determined?
- [ ] Retirement plan documents — SEP, SIMPLE, Solo 401(k), defined benefit

### Deduction Documentation
- [ ] Mortgage interest (Form 1098) — primary and secondary residence
- [ ] Property tax statements — all properties
- [ ] State/local income or sales tax paid — for SALT deduction
- [ ] Charitable contributions — cash (receipts), non-cash (appraisals for items over $5,000), QCDs
- [ ] Medical expenses — total out-of-pocket (only matters if exceeding 7.5% AGI floor)
- [ ] Student loan interest (Form 1098-E)
- [ ] Tuition paid (Form 1098-T) — education credits
- [ ] Child care expenses — provider EIN, amounts paid
- [ ] HSA contributions and distributions (Form 5498-SA, 1099-SA)
- [ ] IRA contributions — traditional (deductible?), Roth, backdoor Roth steps
- [ ] 529 contributions — state deduction availability
- [ ] Casualty/theft losses — FEMA-declared disaster areas only (post-TCJA)

### Life Events (Current and Recent Years)
- [ ] Marriage or divorce — filing status change, alimony (pre/post-2019 matters)
- [ ] Children born or adopted — dependent credits, adoption credit
- [ ] Children aging out — turned 17 (CTC change), turned 19/24 (dependent status)
- [ ] Home purchase or sale — basis, closing statements, exclusion eligibility (2 of 5 year rule)
- [ ] Business started or closed — start date, startup costs, entity selection
- [ ] Business or asset sale — sale price, basis, installment sale consideration
- [ ] Inheritance received — stepped-up basis documentation, estate tax paid (IRD)
- [ ] Relocation — new state filing requirements, moving expenses (military only post-TCJA)
- [ ] Retirement — Social Security timing, RMD requirements (age 73+), pension elections
- [ ] Death of spouse — filing status rules (2-year window for QSS), stepped-up basis

### Estimated Tax & Withholding
- [ ] Current withholding levels — check last pay stub or W-4 on file
- [ ] Estimated payment history — amounts and dates for all quarters
- [ ] Prior year safe harbor status — did payments cover 100% of prior year tax (110% if AGI > $150K)?
- [ ] Underpayment penalty exposure — any quarters significantly short?

---

## Metrics to Extract

### Income Summary
| Metric | What to Extract | Why It Matters |
|--------|----------------|----------------|
| Total gross income | All sources, all filers | Baseline — determines bracket, phase-outs, and strategy options |
| AGI (Adjusted Gross Income) | Line 11 on 1040 | Controls eligibility for most credits and deductions |
| Taxable income | After deductions | Actual number the tax is calculated on |
| Effective tax rate | Total tax ÷ Gross income | Real tax burden — compare to marginal rate |
| Marginal tax rate | Federal bracket + state bracket + SE tax if applicable | What the next dollar costs |
| Income composition | W-2 vs. 1099 vs. K-1 vs. investment vs. passive | Different types have different planning opportunities |

### Business-Specific (if applicable)
| Metric | What to Extract | Why It Matters |
|--------|----------------|----------------|
| Gross revenue | Total business income | Scale determines strategy options |
| Net profit margin | Net income ÷ Gross revenue | Profitability — also determines SE tax base |
| Self-employment tax | Schedule SE total | Often the largest tax surprise for business owners |
| S-corp reasonable comp | Officer salary ÷ Total distributions | IRS scrutiny zone — salary too low triggers audit risk |
| QBI deduction taken? | Section 199A — 20% of qualified business income | Missed by many preparers, especially with multiple entities |
| Retirement contributions | Total across all plan types | Biggest lever for high-income business owners |
| Vehicle deduction method | Standard mileage vs. actual expenses | One may be significantly better — check both |
| Home office deduction | Simplified vs. regular method | Often underclaimed or not claimed at all |
| Depreciation method | Straight-line vs. accelerated vs. Section 179 vs. bonus | Timing of deductions — may have been suboptimal in prior years |

### Deduction Analysis
| Metric | What to Extract | Why It Matters |
|--------|----------------|----------------|
| Standard vs. itemized | Which was used, and by how much did it win? | If close to the threshold, bunching strategy may help |
| SALT deduction | State/local taxes claimed (capped at $10K) | If over cap, SALT workarounds may apply (PTET election) |
| Charitable giving method | Cash, appreciated stock, DAF, QCD | Appreciated stock donations avoid capital gains — often missed |
| Mortgage interest | Amount deducted, acquisition debt vs. HELOC | Post-TCJA rules limit what's deductible |
| Medical expenses | Total vs. 7.5% AGI floor | Usually doesn't clear the floor — but check surgery years |

### Credits Check
| Credit | Eligibility Threshold | What to Verify |
|--------|----------------------|----------------|
| Child Tax Credit | AGI phase-out: $200K single / $400K MFJ | All qualifying children claimed? |
| Child & Dependent Care Credit | Earned income required, $3K/$6K limit | Was it claimed? |
| Education Credits (AOTC/LLC) | MAGI limits, 4-year AOTC cap | AOTC is partially refundable — better than LLC |
| Earned Income Credit | Income limits, investment income limit | Often missed by self-employed with variable income |
| Saver's Credit | AGI under $36.5K single / $73K MFJ (2024) | Low-income filers with retirement contributions |
| EV Credit | Vehicle and income eligibility | New rules post-IRA — point of sale transfer |
| Energy Credits | Home improvements — 25C, 25D | Solar, heat pumps, insulation, windows |
| Premium Tax Credit | Marketplace insurance, ACA subsidies | Reconcile against actual income — overpayment risk |

---

## Contradictions to Check

These are common discrepancies in tax data. Flag every one you find.

### Income
- **1099-K total vs. reported revenue** — If 1099-K shows $200K but Schedule C shows $150K, where's the $50K? Could be returns/refunds (legitimate) or underreporting (problem)
- **K-1 income vs. cash received** — K-1 reports taxable income, not cash distributions. A partner can owe tax on income they never received in cash. Flag if distributions are significantly different from taxable K-1 income
- **Multiple 1099s for same income** — Platform payments sometimes generate both 1099-K and 1099-NEC for the same income. Cross-reference to prevent double-reporting
- **IRS transcript vs. filed return** — If wage & income transcript shows income sources not on the return, this is an unreported income issue. If the return shows income not on the transcript, check if 1099s were simply not issued

### Business
- **S-corp salary vs. distributions** — If officer takes $40K salary and $250K distributions, the salary is almost certainly too low. No bright-line rule, but disproportionate ratios draw IRS attention
- **Business expenses vs. industry norms** — Meals at 40% of revenue? Travel at 25%? Flag outliers — they're either miscategorized or aggressive
- **Vehicle: 100% business use claimed** — Almost never defensible unless the vehicle is a work truck that never goes home. If personal vehicle, 100% business use will not survive audit
- **Home office claimed but also renting office space** — Both can be legitimate (different businesses, days split), but flag for verification
- **Contractors paid but no 1099s issued** — If business deducted payments to individuals over $600 but didn't file 1099s, this is a compliance failure with penalties

### Deductions
- **Charitable donations high relative to income** — Cash donations over 60% AGI or total deductions over 50% AGI trigger scrutiny. Non-cash donations over $5,000 without appraisal are disallowable
- **Standard deduction taken but itemizing would have been better** — Compare both. Preparers sometimes default to standard without checking
- **Itemizing but standard would have been better** — Less common but happens, especially post-TCJA when SALT cap pushed many filers to standard
- **SALT deduction at exactly $10,000** — Correct if they paid more than $10K (hitting the cap). But verify the underlying amount — sometimes state taxes were actually less

### Entity Structure
- **LLC filing as sole prop when S-corp election would save SE tax** — If Schedule C net income exceeds ~$50-60K, S-corp election usually saves money. Was this evaluated?
- **S-corp election in place but no payroll running** — This is a compliance failure. S-corp requires reasonable compensation via payroll
- **Multiple entities with no clear purpose** — Each entity has filing costs and compliance burden. Are they all necessary, or were they created for a reason that no longer applies?
- **State nexus issues** — Income earned in multiple states but only filing in one. Remote work, rental properties in other states, and multistate business activity create filing obligations

### Estimated Taxes
- **Large balance due at filing** — If owing more than $1,000, estimated payments were likely insufficient. Check safe harbor: did they pay 100% of prior year tax (110% if AGI > $150K)?
- **Overpaying estimates significantly** — Giving the IRS a large interest-free loan. Could redirect excess to retirement accounts or investments
- **Uneven quarterly payments** — If income is seasonal, annualized installment method may reduce or eliminate penalty on uneven payments

---

## Common Claims Without Evidence

| Common Claim | What Data Would Verify It |
|-------------|--------------------------|
| "My CPA handles everything, I'm sure it's fine" | Review the actual returns — "handles everything" often means "files what I give them without proactive planning" |
| "I can't contribute more to retirement — I need the cash" | Cash flow analysis — often the tax savings partially fund the contribution |
| "I don't make enough to worry about tax planning" | SE tax alone is 15.3% on first $168.6K (2024). Even $60K net income = ~$9K in SE tax that may be reducible |
| "I take the standard deduction so there's nothing to optimize" | Standard deduction is an itemizing question — above-the-line deductions (retirement, HSA, SE health insurance, SE tax deduction) reduce AGI regardless |
| "My business doesn't make a profit so I don't owe taxes" | Check if losses are being used correctly — hobby loss rules, passive activity limits, at-risk rules may limit deductions |
| "I don't need to file in other states" | Check for rental properties, remote work, K-1s with state withholding, and business activity in other states |
| "I already maxed out my retirement contributions" | Which account? 401(k) limit ≠ SEP limit ≠ defined benefit limit. Multiple plan types can be stacked |
| "I can't do a Roth because I make too much" | Backdoor Roth IRA has no income limit — but check for pro-rata issues (existing traditional IRA balances) |
| "My rental property is a tax shelter" | Check if passive losses are actually being deducted or suspended. Real estate professional status? Active participation? MAGI under $150K for $25K allowance? |
| "I donated a lot to charity" | Cash receipts? Written acknowledgment for gifts over $250? Appraisal for non-cash over $5,000? Substantiation requirements are strict |

---

## Planning Opportunities to Flag

When you find these situations in the data, flag them as potential recommendations for Phase 2. Don't recommend — just note the opportunity exists. For each opportunity, indicate which risk positions are available:

| Position | What It Means | Authority Required |
|----------|--------------|-------------------|
| **Aggressive** | Maximizes tax benefit, higher audit risk, may rely on Tier 4-6 authority or novel interpretation | Must disclose the authority gap explicitly |
| **Moderate** | Defensible position supported by Tier 2B-3 authority, standard practitioner approach | Must cite specific guidance |
| **Conservative** | Safest position, supported by Tier 1-2A authority, minimal audit risk | Must cite statute or regulation |

If only one position exists (e.g., a clear statutory rule), state that. The three-position framing is for situations where judgment is involved.

### Income Shifting / Timing
- Income bunching or deferral opportunities (especially for variable income)
- Roth conversion opportunities (low-income years, pre-RMD years)
- Capital gain harvesting in 0% bracket ($47.0K single / $94.0K MFJ for 2024)
- Tax-loss harvesting — unrealized losses in brokerage accounts

### Business Structure
- Entity election changes (sole prop → S-corp, partnership → S-corp)
- Reasonable compensation optimization for existing S-corps
- Accountable plan setup for employee business expenses
- Augusta Rule (rent primary home to business for 14 days tax-free)

### Retirement
- SEP IRA → Solo 401(k) conversion (higher contribution limits, Roth option)
- Defined benefit plan addition for high-income professionals
- Mega backdoor Roth (if 401(k) plan allows after-tax contributions)
- Catch-up contribution eligibility (age 50+)

### Real Estate
- Cost segregation study for rental properties (accelerate depreciation)
- 1031 exchange eligibility for planned property sales
- Short-term rental material participation (STR loophole for passive loss utilization)
- Section 121 exclusion planning (timing of sale vs. residency)

### Charitable
- Donor Advised Fund (DAF) for bunching strategy
- Qualified Charitable Distribution (QCD) for age 70½+ with IRA
- Donating appreciated stock instead of cash (avoid capital gains)
- Conservation easements (legitimate ones — not syndicated)

---

## Cross-Model Verification Flag

For any finding where tax liability exceeds $50K or involves penalty exposure, flag for **CROSS-MODEL VERIFICATION** before classifying as a VERIFIED FINDING. This means the human reviewer should independently verify the conclusion and citation — not just accept the AI's output. This is especially critical for:
- Positions that rely on novel interpretation of existing authority
- Multi-entity structures where interaction effects create unexpected liability
- Cross-border or multi-state issues where jurisdiction conflicts exist
- Any position that would be classified as "aggressive" in the three-position framing

---

## What This Checklist Does NOT Cover

- Return preparation or filing (this is discovery and planning, not compliance)
- Tax court precedent analysis or legal opinions
- International tax beyond basic FBAR/FATCA flagging
- Estate and gift tax planning (separate domain — could be its own checklist)
- State-specific credits and incentives (too variable — flag for state-specific research)
- Payroll tax optimization beyond S-corp reasonable comp
- Sales tax, excise tax, or property tax (income tax focus only)
- Audit representation or IRS dispute resolution
- Multi-LLM orchestration and consensus analysis (separate process, not a checklist concern)
