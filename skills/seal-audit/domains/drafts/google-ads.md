# SEAL Domain Checklist: Google Ads / GA4

Use this checklist alongside `/seal-audit` when auditing a Google Ads account and/or GA4 property.

---

## Data Sources to Inventory

### Google Ads
- [ ] Campaign performance report — impressions, clicks, CTR, CPC, conversions, cost, ROAS
- [ ] Ad group performance report
- [ ] Keyword performance report — including Quality Score components
- [ ] Search terms report — actual queries triggering ads
- [ ] Auction insights report — competitive landscape
- [ ] Change history — what was modified and when
- [ ] Conversion actions setup — what counts as a conversion, values assigned
- [ ] Bid strategy report — what strategies are in use, performance vs. targets
- [ ] Placement report (if Display/YouTube) — where ads are showing
- [ ] Audience report — demographics, in-market, custom segments
- [ ] Ad copy/creative report — which ads are running, approval status, performance

### GA4
- [ ] Traffic acquisition report — source/medium breakdown
- [ ] Landing page report — engagement and conversion by page
- [ ] Conversion path report — multi-touch attribution
- [ ] User explorer / cohort data — if available
- [ ] Audience overlap — are campaigns competing for the same users
- [ ] Event tracking setup — what events are configured, are they firing correctly

### Supporting
- [ ] Landing pages — URLs, load time, mobile experience
- [ ] CRM or lead tracking — what happens after the conversion event
- [ ] Revenue data — actual sales vs. reported conversion values

---

## Metrics to Extract

### Account Structure
| Metric | What to Extract |
|--------|----------------|
| Campaign count | Total campaigns, active vs. paused |
| Ad group count | Groups per campaign, keyword themes |
| Match type distribution | Broad vs. phrase vs. exact — % of spend by match type |
| Bid strategies in use | Manual CPC, Target CPA, Target ROAS, Maximize conversions, etc. |
| Budget allocation | Daily budgets vs. actual spend by campaign |
| Impression share | Search IS, lost IS (budget), lost IS (rank) |

### Performance
| Metric | What to Extract | Benchmark Range |
|--------|----------------|-----------------|
| CTR | Click-through rate by campaign/ad group | 3-5%+ (search), varies by industry |
| CPC | Average cost per click | Industry-dependent |
| Conversion rate | Conversions ÷ Clicks | 3-5%+ (search) |
| Cost per conversion | Spend ÷ Conversions | Industry-dependent |
| ROAS | Conversion value ÷ Spend | Business-dependent |
| Quality Score | Keyword-level QS distribution | 7+ is good, below 5 is a problem |
| QS components | Expected CTR, ad relevance, landing page experience | Above average for each |

### Waste
| Metric | What to Extract |
|--------|----------------|
| Irrelevant search terms | Queries triggering ads that don't match intent |
| Negative keyword gaps | Missing negatives that would prevent wasted clicks |
| Low QS keywords still spending | Keywords with QS below 4 that are consuming budget |
| Bad placements (Display) | Sites/apps/channels with high spend and no conversions |

---

## Contradictions to Check

| Check | What to Compare |
|-------|----------------|
| Google Ads conversions vs. GA4 conversions | Mismatches are common — different attribution models, conversion windows, counting methods |
| Reported ROAS vs. actual revenue | Are conversion values in Google Ads accurate? Check against actual sales data |
| Impression share vs. budget | Is the campaign limited by budget or by rank? Different diagnoses |
| Campaign-level CPA vs. ad group CPA | Averages hide problems — one ad group may be dragging the campaign average |
| "Conversions" definition | Are phone calls, form fills, and purchases all counted as the same "conversion"? Weighted the same? |
| Change history vs. performance shifts | Did performance change when someone made an account change? Timeline the correlation |
| Claimed target audience vs. actual converting audience | Demographics and search terms of actual converters vs. who the client thinks they're targeting |

---

## Common Claims Without Evidence

| Common Claim | What Data Would Verify It |
|-------------|--------------------------|
| "Our Google Ads aren't working" | Define "working" — what CPA or ROAS target? Compare actual vs. target |
| "We need more budget" | Check impression share lost to budget — if IS is already 90%+, more budget won't help much |
| "Our competitors are outbidding us" | Auction insights — actual overlap rate and outranking share |
| "Brand campaigns are wasting money" | Brand vs. non-brand split — what % of conversions are brand? Would you lose those without ads? |
| "We tried broad match and it didn't work" | Search terms report for the broad match period — was it the match type or the lack of negatives? |
| "Our landing page is fine" | QS landing page component, GA4 bounce/engagement rate, conversion rate vs. benchmarks |
| "We need new keywords" | Check existing keyword coverage first — are current keywords maxed out on impression share? |
