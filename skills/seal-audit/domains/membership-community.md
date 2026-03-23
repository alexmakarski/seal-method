# SEAL Domain Checklist: Membership / Community / Subscription

Use this checklist alongside `/seal-audit` when auditing a membership community, paid community, or subscription-based knowledge/networking business (Skool, Circle, Mighty Networks, custom-built, etc.).

---

## Data Sources to Inventory

### Financial / Accounting
- [ ] P&L — monthly, last 12 months minimum
- [ ] Revenue by tier/plan — what each membership level generates
- [ ] Revenue by payment frequency — monthly vs. annual vs. lifetime
- [ ] Failed payment / dunning data — involuntary churn from card failures
- [ ] Refund history — volume, timing (day 3 vs. day 25), reasons if captured
- [ ] COGS / delivery cost — platform fees, content production, moderation, support
- [ ] Payroll / contractor detail — community managers, content creators, moderators, support
- [ ] Software/tool costs — community platform, email, video hosting, course hosting, integrations
- [ ] Revenue from non-membership sources — events, courses, coaching, sponsorships, affiliate

### Membership / Subscriber Data
- [ ] Total active members — current count, definition of "active"
- [ ] Member roster with join dates — needed for cohort analysis
- [ ] Cancellation data with dates and reasons — if captured
- [ ] Tier/plan distribution — how many members at each price point
- [ ] Payment history — MRR trend, monthly/annual split
- [ ] Trial/free tier data — how many, conversion rate to paid
- [ ] Founding member or legacy pricing — how many are on old rates
- [ ] Geographic distribution — relevant for time zones, events, pricing sensitivity

### Engagement / Activity
- [ ] Login frequency — daily/weekly/monthly active members
- [ ] Content consumption — what gets viewed, completed, bookmarked
- [ ] Community participation — posts, comments, replies per member per period
- [ ] Event attendance — live calls, workshops, Q&As (registered vs. attended)
- [ ] Resource/tool usage — templates, calculators, directories, databases
- [ ] Direct messages / peer connections — if trackable
- [ ] Power user identification — who are the top 5-10% by activity
- [ ] Ghost member count — paying members with zero activity in 60+ days

### Acquisition / Growth
- [ ] New member sources — organic, paid, referral, affiliate, partnership, event-driven
- [ ] Acquisition cost per member — by channel if possible
- [ ] Conversion funnel — visitor → trial → paid (or visitor → paid), with drop-off rates
- [ ] Sales page / landing page — current version, conversion rate if tracked
- [ ] Email list size vs. member count — what's the unconverted list?
- [ ] Launch history — did membership grow via launches or evergreen?
- [ ] Referral/affiliate program — if exists, performance data
- [ ] Social proof inventory — testimonials, case studies, member stories

### Onboarding / Activation
- [ ] Onboarding sequence — what happens in first 7/14/30 days
- [ ] Activation metrics — what action correlates with retention (if known)
- [ ] Welcome flow — emails, DMs, community introductions
- [ ] Time to first value — how quickly a new member gets what they came for
- [ ] Onboarding completion rate — if structured onboarding exists

### Content / Curriculum
- [ ] Content library inventory — courses, lessons, resources, templates
- [ ] Content freshness — when was each piece last updated
- [ ] Content production cadence — how often is new material added
- [ ] Content format mix — video, text, audio, templates, tools
- [ ] Live vs. evergreen ratio — how much requires the founder to show up
- [ ] Curriculum structure — is there a clear learning path or is it a library?

### Community Health
- [ ] Ratio of creator-generated vs. member-generated content
- [ ] Response time to member questions
- [ ] Moderation load — spam, disputes, off-topic
- [ ] Sub-group/channel activity — which spaces are alive vs. dead
- [ ] Member sentiment — NPS, surveys, exit interviews
- [ ] Success stories — documented wins, transformations

### Retention / Churn
- [ ] Monthly churn rate — cancellations ÷ starting member count
- [ ] Churn by cohort — do members who joined in January retain differently than July?
- [ ] Churn by tier — do higher-paying members stay longer?
- [ ] Voluntary vs. involuntary churn — cancellations vs. failed payments
- [ ] Cancellation reasons — if collected (survey, exit interview)
- [ ] Average member lifetime — in months
- [ ] Retention curve — what % remain at 3/6/12/24 months
- [ ] Win-back attempts — has anyone tried to re-engage churned members?

---

## Metrics to Extract

### Financial Health
| Metric | What to Extract | Benchmark Range |
|--------|----------------|-----------------|
| MRR | Monthly recurring revenue (normalize annual to monthly) | Context-dependent |
| ARR | MRR × 12 | Context-dependent |
| Revenue per member | MRR ÷ Active members | Context-dependent |
| Gross margin | (Revenue - direct delivery costs) ÷ Revenue | 70-85%+ |
| Net profit margin | Net income ÷ Revenue | 30-50%+ (community businesses should be high margin) |
| LTV | Average revenue per member × average lifetime in months | Should be 3x+ CAC |
| LTV:CAC ratio | Lifetime value ÷ Customer acquisition cost | 3:1 minimum, 5:1+ healthy |
| Payback period | CAC ÷ Monthly revenue per member | Under 3 months ideal |
| Non-membership revenue % | Other revenue ÷ Total revenue | Flag if over 50% — is this really a membership business? |

### Growth
| Metric | What to Extract | Benchmark Range |
|--------|----------------|-----------------|
| Monthly net member growth | New members - churned members | Positive = growing |
| Monthly growth rate | Net new ÷ Starting count | 5-10% monthly is strong |
| New members per month | Raw count, trailing 3-month average | Context-dependent |
| Acquisition cost | Total acquisition spend ÷ New members | Must be < LTV/3 |
| Conversion rate (visitor → member) | New members ÷ Sales page visitors | 2-10% depending on traffic quality |
| Email list conversion | Members ÷ Total list size | Context-dependent |
| Referral rate | % of new members from referrals | Higher = healthier |

### Engagement
| Metric | What to Extract | Benchmark Range |
|--------|----------------|-----------------|
| DAU/MAU ratio | Daily active ÷ Monthly active | 20-30%+ is strong for community |
| WAU/MAU ratio | Weekly active ÷ Monthly active | 40-60%+ |
| Posts per active member per month | Community contributions ÷ Active members | Context-dependent |
| Event attendance rate | Attendees ÷ Registered (or ÷ Total members) | 15-30% of membership is healthy |
| Content completion rate | Finished ÷ Started (for courses/programs) | 30%+ |
| Ghost member rate | Zero-activity members ÷ Total members | Under 30% is healthy; over 50% is a churn time bomb |

### Retention
| Metric | What to Extract | Benchmark Range |
|--------|----------------|-----------------|
| Monthly churn rate | Cancellations ÷ Starting member count | Under 5% monthly |
| Annual churn rate | 1 - (1 - monthly churn)^12 | Under 40% annual |
| 90-day retention | % of cohort still active at 90 days | 70%+ |
| 12-month retention | % of cohort still active at 12 months | 40%+ |
| Average member lifetime | 1 ÷ Monthly churn rate (in months) | 12+ months |
| Involuntary churn rate | Failed payments not recovered ÷ Total members | Under 2% monthly |
| Net revenue retention | Revenue from existing members this month ÷ Same members last month | 100%+ means upsell > churn |

---

## Contradictions to Check

### Financial
- **"We're growing" vs. MRR trend** — Member count can grow while MRR shrinks if new members join at lower tiers or older high-paying members churn. Check MRR, not just headcount
- **High revenue but founder-dependent delivery** — If removing the founder from live calls, content creation, and community engagement would collapse the business, this is a job with subscribers, not a scalable membership
- **"High margin business" vs. hidden labor** — Is the founder's daily community engagement, content production, and member support costed in? Add market-rate salary for all founder hours and recalculate
- **Annual revenue looks healthy vs. monthly cash flow** — If most members are annual, revenue is lumpy. A bad renewal month can create cash crunches
- **Multiple revenue streams vs. subsidization** — The membership may be subsidized by coaching, courses, or events. Strip each stream out — is the membership profitable standalone?

### Engagement & Retention
- **"Our community is active" vs. engagement data** — Active could mean 10 power users carrying the whole community while 80% are ghosts. Check the distribution, not the average
- **High engagement but high churn** — Members participate actively then leave. The value might be extractable — they get what they need and go. This isn't necessarily bad, but the business model must account for it
- **"People love it" vs. NPS/exit data** — Testimonials from power users don't represent the silent majority. What do people say when they cancel?
- **Low churn claimed vs. cohort analysis** — Monthly churn can look low if you're adding members fast. Check cohort curves — what happens to the January joiners by June?
- **"We have great content" vs. consumption data** — A 200-lesson library where members only watch 5 lessons isn't great content — it's content bloat. What actually gets used?

### Growth
- **"We grow through referrals" vs. referral tracking** — If there's no formal referral mechanism or tracking, "referrals" means "we don't know where members come from"
- **Launch-driven growth vs. evergreen sustainability** — Big member spikes during launches followed by elevated churn = a launch business, not a subscription business. Check the 90-day retention of launch cohorts vs. evergreen signups
- **"We don't need to advertise" vs. growth rate** — Organic growth is great until it isn't. If the community needs to grow and has no paid acquisition channel, there's no throttle to control
- **Low CAC claimed vs. actual investment** — Organic content creation, podcast episodes, social media, speaking gigs, free workshops — all have a cost in time. Are these acquisition costs being tracked?

### Community
- **Peer-to-peer value vs. top-down dependency** — Is value created by members interacting, or by the founder/team answering questions? The former scales; the latter doesn't
- **"Community" vs. content library with comments** — A true community has member-to-member connections. A content library with a comment section is a different product. Which is this?
- **Multiple tiers vs. tier confusion** — More tiers doesn't mean more revenue if members can't tell the difference. Check upgrade rates between tiers and whether higher tiers actually deliver differentiated value

---

## Common Claims Without Evidence

| Common Claim | What Data Would Verify It |
|-------------|--------------------------|
| "We have X members" | Active, paying members — not total signups, not including cancelled, not free tier |
| "Our churn is low" | Monthly churn rate with actual calculation. "Low" compared to what? |
| "Members stay for years" | Average lifetime calculation from cohort data, not anecdotes about founding members |
| "The community sells itself" | Referral tracking, word-of-mouth attribution, viral coefficient |
| "Our content is best in class" | Consumption data, completion rates, member feedback on content vs. community vs. network value |
| "We could charge more" | Price sensitivity testing, competitor pricing analysis, willingness-to-pay data |
| "Members get 10x the value" | Documented ROI stories, before/after metrics, member-reported outcomes |
| "We're building a moat" | Switching costs analysis — what would a member lose by leaving that they can't get elsewhere? |
| "The community is self-sustaining" | What % of content/value comes from members vs. staff? Would activity drop if staff stopped posting for 30 days? |
| "We just need more traffic" | Current conversion rate × additional traffic = projected growth. But does churn eat it? |

---

## Membership Model Analysis

### Pricing Model
| Model | What to Check | Risk |
|-------|--------------|------|
| Single tier, monthly | Simple, low friction entry | Limited upsell; revenue only grows with headcount |
| Multiple tiers | Tier differentiation, upgrade rates | Complexity, cannibalization between tiers |
| Annual only | Higher commitment, better cash flow | Higher barrier to entry, lumpy renewals |
| Monthly + annual | Discount for annual incentivizes commitment | Monthly members may churn before converting to annual |
| Lifetime deal | Cash injection | Destroys LTV, creates perpetual obligation |
| Free + premium | Freemium funnel | Free tier may satisfy enough — low conversion to paid |

### Structural Risks to Flag
- **Founder dependency** — If the founder is the primary content creator, community engager, and face of the brand, this is a personal brand with a subscription, not a standalone community business
- **Platform dependency** — Community lives on one platform (Skool, Facebook Group, etc.) with no owned data export. Platform changes or shutdown = existential risk
- **Content treadmill** — Must produce new content constantly to justify ongoing subscription. No evergreen value that compounds
- **Network effects not present** — Members join for content, not for each other. Without network effects, this is a subscription content product competing with free content everywhere
- **No activation trigger identified** — If you don't know what action in the first 14 days predicts retention, you can't optimize onboarding
- **Ghost member subsidization** — Business depends on members who pay but don't use the product. This is a revenue model, not a value model. It works until it doesn't

---

## What This Checklist Does NOT Cover

- Individual content quality assessment (courses, lessons, templates)
- Platform-specific technical optimization (Skool SEO, Circle features, etc.)
- Legal review of membership terms, refund policies, or data handling
- Individual member success analysis
- Content creation strategy or editorial calendar planning
- Community moderation playbook design
