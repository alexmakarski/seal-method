# SEAL Domain Checklist: Marketing Data Readiness

Use this checklist alongside `/seal-audit` when assessing whether a company's marketing data infrastructure can support AI tools, automation, and intelligent decision-making. This checklist diagnoses the data foundation — not the AI tools themselves.

**When to use:** When a company is deploying (or has failed to deploy) AI-powered marketing tools — attribution, bid optimization, audience targeting, content personalization, predictive analytics, synthetic panels — and results are disappointing or inconsistent.

**Core thesis:** Most marketing AI failures are data failures. The model isn't wrong — the data feeding it is fragmented, stale, ungoverned, or disconnected. This checklist finds where the data breaks before blaming the AI.

---

## Data Sources to Inventory

### Marketing Platform Data (the execution layer)
- [ ] Ad platforms in use — Google Ads, Meta Ads, TikTok, LinkedIn, Tier 2 networks, programmatic DSPs
- [ ] Number of ad platforms actively running spend — and whether data from ALL of them flows into a single view
- [ ] Email/marketing automation platform — Klaviyo, HubSpot, ActiveCampaign, Mailchimp, etc.
- [ ] SMS/push platform — Attentive, Postscript, OneSignal, etc.
- [ ] Social media management — Sprout, Hootsuite, native platforms
- [ ] Content management — WordPress, Shopify CMS, headless CMS, etc.
- [ ] Landing page tools — Unbounce, Instapage, custom builds

### Customer Data Infrastructure (the identity layer)
- [ ] CRM — HubSpot, Salesforce, Attio, Pipedrive, etc.
- [ ] CDP — Segment, mParticle, Rudderstack, Tealium, or none
- [ ] Customer data warehouse — BigQuery, Snowflake, Redshift, Databricks, or none
- [ ] Identity resolution — unified customer ID across platforms? 5x5, LiveRamp, custom?
- [ ] Consent management — OneTrust, Cookiebot, custom, or nothing
- [ ] Data enrichment — Clearbit, ZoomInfo, 5x5, Apollo, or none

### Analytics & Measurement (the truth layer)
- [ ] Web analytics — GA4, Adobe Analytics, Plausible, Fathom, Amplitude
- [ ] Attribution tool — TripleWhale, Northbeam, Rockerbox, platform-native, or none
- [ ] Conversion tracking — server-side vs. client-side, CAPI implementation status
- [ ] Revenue source of truth — Stripe, Shopify, ERP, QuickBooks, or whatever the business considers "real revenue"
- [ ] Call tracking — CallRail, Invoca, or none (if leads come through phone)
- [ ] Heatmaps/session recording — Hotjar, FullStory, Lucky Orange, or none

### Data Movement (the plumbing)
- [ ] ETL/ELT tool — Fivetran, Airbyte, Stitch, custom scripts, manual exports, or nothing
- [ ] Data integration method — API connections, CSV exports, Zapier/Make, manual copy-paste
- [ ] Reporting layer — Looker, Tableau, Power BI, Google Sheets, platform-native dashboards
- [ ] How frequently does data refresh? — Real-time, hourly, daily, weekly, "whenever someone runs a report"
- [ ] Who maintains the data pipelines? — Dedicated data person, marketing team, agency, nobody

### AI Tools Already Deployed (what's trying to use this data)
- [ ] AI bid management — Google Performance Max, Meta Advantage+, third-party
- [ ] AI content/creative — Jasper, ChatGPT, Midjourney, brand-specific tools
- [ ] Predictive analytics — churn prediction, LTV forecasting, lead scoring
- [ ] Personalization engine — Dynamic Yield, Optimizely, platform-native
- [ ] Synthetic validation — SimPanel, or equivalent
- [ ] Custom AI/ML models — any internally built models consuming marketing data

---

## Metrics to Extract

### Data Completeness
| Metric | What to Extract | Red Flag |
|--------|----------------|----------|
| Platform coverage | % of ad spend that feeds into a unified data view | Below 80% = blind spots in AI inputs |
| Customer record completeness | % of customer records with email + name + at least one purchase | Below 60% = identity resolution problems |
| Conversion tracking coverage | % of revenue-generating events that are tracked end-to-end | Below 90% = attribution is lying |
| Historical data depth | Months of clean, queryable historical data available | Under 12 months = insufficient training data for any AI model |
| Cross-platform ID match rate | % of customers identifiable across 2+ platforms | Below 30% = no unified customer view |

### Data Freshness
| Metric | What to Extract | Red Flag |
|--------|----------------|----------|
| Reporting lag | Hours/days between event and when it appears in analytics | Over 24 hours for ad spend data = decisions based on stale data |
| CRM sync frequency | How often CRM updates from marketing platforms | Manual or weekly = pipeline data is always wrong |
| Audience refresh rate | How often custom audiences update with new data | Over 7 days = targeting yesterday's customer |
| Attribution window alignment | Do all platforms use the same attribution window? | Mismatched windows = the same conversion counted differently everywhere |

### Data Consistency
| Metric | What to Extract | Red Flag |
|--------|----------------|----------|
| Revenue discrepancy | Difference between platform-reported revenue and actual revenue (Stripe/Shopify/ERP) | Over 15% gap = AI is optimizing toward wrong numbers |
| Conversion count discrepancy | Google Ads conversions vs. GA4 vs. CRM vs. actual sales | Discrepancies over 20% across any pair |
| Customer count discrepancy | Marketing platform audience size vs. CRM contacts vs. actual buyers | Large gaps = duplicate records, bad deduplication, or phantom contacts |
| UTM/tracking consistency | % of campaigns with complete, consistent UTM parameters | Below 80% = attribution gaps, "direct/none" bucket is inflated |
| Naming convention compliance | Do campaigns follow a consistent naming structure across platforms? | No naming convention = impossible to aggregate cross-platform data reliably |

### Data Governance
| Metric | What to Extract | Red Flag |
|--------|----------------|----------|
| Data owner | Is there a named person responsible for data quality? | "Nobody" or "everybody" = nobody |
| Documented data dictionary | Does a document exist defining what each metric means? | No dictionary = everyone interprets "conversion" differently |
| Data quality monitoring | Are there alerts when pipelines break or data anomalies occur? | No monitoring = problems discovered weeks later when reports look wrong |
| Privacy compliance | GDPR/CCPA consent records, data deletion capability, opt-out tracking | No consent management = legal risk AND dirty data (opted-out users in audiences) |
| Access controls | Who can edit tracking, change conversion definitions, modify audiences? | Everyone = nobody is accountable for data changes |

### Integration Health
| Metric | What to Extract | Red Flag |
|--------|----------------|----------|
| Total marketing platforms in use | Count all tools in the martech stack | 17-20 is average; above 25 with no integration layer = data chaos |
| Connected vs. siloed platforms | How many platforms push/pull data to a central system? | Below 50% connected = more data is trapped than shared |
| Manual data processes | How many regular reports require manual data pulls, CSV exports, or copy-paste? | Any critical business metric that requires manual assembly = fragile and error-prone |
| API utilization | How many platforms are connected via API vs. manual export? | Heavy reliance on CSV/manual = data is always late and sometimes wrong |
| Single source of truth existence | Is there ONE place where all marketing data converges for reporting? | No SSOT = different teams see different numbers, make conflicting decisions |

---

## Contradictions to Check

### The AI Tool Isn't Working vs. The Data Is Broken
- **"Our AI attribution tool gives bad recommendations"** vs. the data feeding it — Is the tool wrong, or is it getting incomplete/conflicting conversion data? Check: are all conversion events tracked? Is revenue data accurate? Are attribution windows consistent?
- **"Performance Max / Advantage+ doesn't work for us"** vs. conversion signal quality — Google and Meta's AI needs clean, complete conversion signals. Check: is server-side tracking implemented? Are conversion values accurate? Are there enough conversions per week for the algorithm to learn (minimum 30-50)?
- **"Our predictive model's accuracy dropped"** vs. data pipeline changes — Did someone change a tracking pixel, rename a campaign, modify a conversion event, or switch analytics platforms without updating the model's data source?

### We Have Good Data vs. Reality
- **"We track everything"** vs. actual conversion path coverage — Check: what happens between the click and the sale? Is there a gap where data is lost (phone calls, in-store, long sales cycles, multiple decision-makers)?
- **"Our CRM is clean"** vs. duplicate rate and completeness — Run a dedup check. How many records have no email? No company name? Were created by a form fill with "asdf" in the name field?
- **"We know our CAC"** vs. what's included in the calculation — Does their CAC include all ad spend? Agency fees? Creative costs? Tool costs? Or just the platform spend divided by conversions?
- **"Our dashboards are accurate"** vs. source data — Do dashboards pull from platforms directly or from a warehouse? If directly, are they comparing apples to oranges across platforms with different attribution models?

### Cross-Platform Conflicts
- **Google Ads ROAS vs. Meta ROAS vs. actual revenue** — Both platforms will claim credit for the same sale. Compare total claimed conversions across all platforms vs. actual total conversions. The gap is the "double-counting tax."
- **Platform audience sizes vs. actual reachable audience** — Meta says your audience is 2M. Google says 1.5M. Your customer list is 50K. Who's right? What does the AI think it's optimizing for?
- **Marketing-reported leads vs. sales-accepted leads** — If marketing says they generated 500 leads but sales only accepted 50, the AI is optimizing for a metric (lead volume) that doesn't correlate with revenue.

### Investment vs. Capability
- **"We invested in a CDP"** vs. what it actually does — Is the CDP receiving data from all sources? Is it resolving identities? Is it pushing audiences back to platforms? Many CDP implementations are half-built — data goes in but nothing useful comes out.
- **"We have a data warehouse"** vs. who queries it — If nobody on the marketing team can access or query the warehouse, it's not a marketing data asset. It's an engineering artifact.
- **"We moved to server-side tracking"** vs. what's actually server-side — Partial CAPI implementation (Meta only, not Google, not TikTok) creates a new inconsistency. One platform gets better data than the others, skewing budget allocation.

---

## Common Claims Without Evidence

| Common Claim | What Data Would Verify It |
|-------------|--------------------------|
| "We have a 360-degree view of our customer" | Show the unified customer record. Can you pull one customer and see: every ad they saw, every email they opened, every page they visited, every purchase they made? If not, it's not 360. |
| "Our data is clean" | Duplicate rate, completeness score (% of records with all key fields populated), recency (% of records updated in last 90 days), accuracy spot-check against source systems |
| "We just need better AI tools" | What data quality score are the current tools getting? Have you validated the inputs before blaming the outputs? |
| "Our attribution is accurate" | Compare platform-reported revenue (summed across all platforms) to actual revenue. If platform total is 2x actual revenue, attribution is theater, not measurement. |
| "We personalize our marketing" | What data drives the personalization? If it's just "first name in subject line" and "abandoned cart email," that's not personalization — it's basic automation. Real personalization requires behavioral + purchase + preference data unified. |
| "We're ready for AI" | Have they passed even a basic data readiness check? Can they answer: where does your data live? Who owns it? How fresh is it? How do you know when it's wrong? |
| "We've invested in our data stack" | Investment doesn't equal readiness. Check: are the tools connected? Is data flowing? Is anyone monitoring quality? Investment without integration is just software licenses. |
| "Our agency handles data" | What specifically does the agency have access to? Do they own the tracking setup? If the agency leaves, does the data infrastructure survive? |
| "We don't have a data problem, we have a strategy problem" | Check the data first. In our experience, companies that say this discover 3-5 data issues in the first hour of a SEAL audit that change the strategic picture entirely. |
| "GA4 is our source of truth" | GA4 is a sampled, modeled, consent-dependent analytics tool. It is NOT a source of truth for revenue. Compare GA4 revenue to Stripe/Shopify/ERP. The gap is usually 15-40%. |

---

## Marketing Data Readiness Score

When enough data is collected, classify the organization into one of four readiness levels:

### Level 1: Fragmented (Not Ready for AI)
**Indicators:**
- Data lives in 10+ platforms with no integration layer
- No unified customer ID across platforms
- Revenue reporting requires manual CSV assembly
- No data quality monitoring — problems discovered by accident
- Different teams use different numbers for the same metric

**Diagnosis:** AI tools deployed here will produce unreliable outputs. The first investment should be data infrastructure, not AI tooling.

**Typical finding:** "Your AI attribution tool isn't wrong — it's being fed conflicting data from three platforms with different conversion definitions and no shared customer ID."

### Level 2: Partially Connected (AI Will Underperform)
**Indicators:**
- Some platforms connected via ETL or API (40-70%)
- CRM exists but has completeness issues (duplicate records, missing fields)
- One analytics platform serves as a semi-reliable reporting layer
- Some conversion tracking gaps (phone calls, in-store, long sales cycles)
- Data refreshes daily but not in real-time

**Diagnosis:** AI tools will work but underperform expectations. The data is "good enough" for basic automation but not for sophisticated optimization. Quick wins available through better integration.

**Typical finding:** "Your bid management AI is optimizing on 70% of your conversion data. The 30% it can't see — phone calls, in-store visits, multi-touch B2B deals — means it's systematically misallocating budget."

### Level 3: Integrated (AI-Ready with Gaps)
**Indicators:**
- 80%+ platforms connected to a central data layer (warehouse or CDP)
- Unified customer ID exists and covers most touchpoints
- Conversion tracking is comprehensive (server-side where needed)
- Data refreshes at least daily, critical metrics hourly
- Named data owner and documented data dictionary
- Revenue discrepancy between platforms and actuals under 15%

**Diagnosis:** AI tools will perform well. Remaining gaps are specific and addressable. Focus on closing the last integration gaps and adding monitoring.

**Typical finding:** "Your data foundation is solid. The gap is in identity resolution — 30% of your cross-platform customers aren't being matched, which means your AI is undervaluing multi-channel journeys."

### Level 4: AI-Optimized (Competitive Advantage)
**Indicators:**
- All critical platforms connected with real-time or near-real-time sync
- Unified customer graph with identity resolution across all touchpoints
- Server-side conversion tracking on all major platforms
- Automated data quality monitoring with alerts
- Single source of truth for revenue, accessible to all teams
- Clean historical data (12+ months) for model training
- Data governance policies in place and enforced

**Diagnosis:** The data infrastructure is a competitive advantage. AI tools deployed here will outperform the same tools deployed by competitors with worse data. Focus on advanced use cases: predictive audiences, real-time personalization, synthetic validation.

**Typical finding:** "Your data stack is better than 90% of your competitors. The opportunity is to deploy tools (SimPanel, predictive LTV, dynamic creative optimization) that competitors literally cannot use because their data won't support it."

---

## Domain-Specific Deep Dives

### The 17-Platform Problem
When the martech stack exceeds 15 platforms, map each one:

| Platform | Category | Connected To | Data Flows In | Data Flows Out | Owner |
|----------|----------|-------------|---------------|----------------|-------|
| (name) | (ad/email/CRM/analytics/etc.) | (what it talks to) | (what data it receives) | (what data it sends) | (who maintains it) |

Flag:
- Platforms that receive data but don't send it anywhere (data black holes)
- Platforms that send data to each other but not to a central system (island networks)
- Platforms nobody maintains but everyone uses (orphan tools)
- Platforms that duplicate another tool's function (tool sprawl)

### Identity Resolution Assessment
| Question | Answer | Impact |
|----------|--------|--------|
| Do you have a unified customer ID? | Yes/No | Without this, all cross-platform analysis is approximate |
| What systems use this ID? | List platforms | Gaps = blind spots |
| How is identity matched? | Deterministic (email match) vs. probabilistic | Probabilistic = some false matches |
| What's your cross-platform match rate? | % of records matched across 2+ platforms | Below 30% = you don't really have a unified view |
| What happens to anonymous visitors? | Tracked, lost, or cookied with degrading accuracy | Most companies lose 60-80% of the customer journey |
| Post-cookie strategy | First-party data focus? Server-side tracking? ID graph? | No strategy = worsening data quality every quarter |

### The Revenue Truth Test
The single most important data quality check for any company deploying marketing AI:

1. Pull total attributed revenue from EVERY ad platform (Google, Meta, TikTok, etc.) — sum them
2. Pull total revenue from the financial source of truth (Stripe, Shopify, ERP)
3. Compare

| Scenario | What It Means |
|----------|--------------|
| Platform total is within 10% of actual | Rare. Data is unusually clean. Verify it's not accidental. |
| Platform total is 1.5-2x actual | Typical. Double-counting across platforms. AI tools optimizing on these numbers are systematically overstating performance. |
| Platform total is 2x+ actual | Severe. Attribution is fiction. Any AI tool optimizing on this data is making decisions based on fantasy. Fix tracking before doing anything else. |
| Platform total is BELOW actual | Tracking gaps — conversions happening that platforms can't see (phone, offline, long sales cycle). AI is under-investing in channels that actually drive revenue. |

---

## What This Checklist Does NOT Cover

- Specific ad platform audit methodology — use `google-ads.md` or platform-specific checklists for that
- Creative quality or messaging strategy
- Marketing strategy, positioning, or audience targeting decisions
- Data engineering implementation (how to build the pipelines) — this checklist diagnoses, it doesn't prescribe architecture
- Legal compliance review (though privacy/consent is flagged as a data quality factor)
- AI model selection or evaluation — this checklist assesses the DATA feeding AI tools, not the tools themselves
