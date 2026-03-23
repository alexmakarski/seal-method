# SEAL Domain Checklist: Dental Practice

Use this checklist alongside `/seal-audit` when auditing a dental practice. This defines what data to look for, what metrics to extract, and what contradictions to check.

---

## Data Sources to Inventory

### Practice Management Software (Dentrix, Eaglesoft, Open Dental, Curve, etc.)
- [ ] Production report by provider (doctor + hygienists) — monthly, last 12 months minimum
- [ ] Collections report — monthly, last 12 months minimum
- [ ] Adjustments/write-offs report — what's being discounted and why
- [ ] New patient count — monthly, last 12 months
- [ ] Active patient count (seen in last 18 months)
- [ ] Scheduled vs. completed appointments (cancellation/no-show rate)
- [ ] Treatment plans presented vs. accepted (case acceptance)
- [ ] Outstanding treatment — patients with unscheduled treatment plans
- [ ] Recall/reactivation report — patients overdue for hygiene
- [ ] Procedure code mix — what procedures are generating revenue (D0-D9 categories)
- [ ] Insurance aging report — outstanding claims by age bucket
- [ ] Patient aging report — outstanding patient balances by age bucket

### Accounting / Bookkeeping (QuickBooks, Xero, CPA reports)
- [ ] P&L — monthly, last 12 months minimum
- [ ] Overhead breakdown: staff wages, lab fees, supplies, facility, insurance, marketing, technology, CE
- [ ] Payroll detail — provider compensation vs. support staff
- [ ] Marketing spend — by channel if available (Google, direct mail, referral programs, etc.)

### Marketing Data
- [ ] Google Business Profile insights — calls, direction requests, website clicks, reviews
- [ ] Google Ads data — if running paid search
- [ ] Website analytics (GA4 or similar) — traffic, form submissions, call clicks
- [ ] Call tracking data — if using CallRail, WhatConverts, etc.
- [ ] Social media metrics — if actively posting/advertising
- [ ] Referral source tracking — how new patients say they found the practice

### Patient Experience
- [ ] Online reviews — Google, Yelp, Healthgrades (count, average rating, recent trend)
- [ ] Patient survey results — if conducted
- [ ] Complaint log — if maintained

### Operational
- [ ] Staff roster — roles, tenure, hours, compensation
- [ ] Hours of operation — current schedule
- [ ] Number of operatories and utilization
- [ ] Equipment age / recent capital expenditures
- [ ] Lease terms — facility cost and expiration

---

## Metrics to Extract

### Financial Health
| Metric | What to Extract | Benchmark Range |
|--------|----------------|-----------------|
| Annual collections | Total collected revenue | Context-dependent |
| Production-to-collections ratio | Collections ÷ Production | 95-98%+ |
| Overhead ratio | Total overhead ÷ Collections | 55-65% |
| Staff cost ratio | Total staff wages ÷ Collections | 25-30% |
| Lab cost ratio | Lab fees ÷ Collections | 8-10% |
| Supply cost ratio | Supplies ÷ Collections | 5-6% |
| Facility cost ratio | Rent/mortgage ÷ Collections | 5-7% |
| Marketing cost ratio | Marketing spend ÷ Collections | 3-5% |
| Doctor compensation % | Doctor take-home ÷ Collections | 30-40% (owner) |
| Hygiene production ratio | Hygiene production ÷ Total production | 25-33% |

### Patient Flow
| Metric | What to Extract | Benchmark Range |
|--------|----------------|-----------------|
| New patients per month | Count from PMS | 20-50+ depending on practice size |
| Active patient count | Seen in last 18 months | Context-dependent |
| Patient attrition rate | Patients lost ÷ Active patients (annual) | Under 15% |
| Recall overdue | Patients past due for hygiene | Under 20% of active |
| Reactivation pool | Patients 18-36 months since last visit | Opportunity metric |

### Case Acceptance
| Metric | What to Extract | Benchmark Range |
|--------|----------------|-----------------|
| Case acceptance rate | Accepted treatment $ ÷ Presented treatment $ | 70-85% |
| Outstanding treatment value | Total $ of unscheduled accepted treatment | Opportunity metric |
| Average treatment plan value | Mean $ of treatment plans presented | Context-dependent |

### Schedule Efficiency
| Metric | What to Extract | Benchmark Range |
|--------|----------------|-----------------|
| Schedule utilization | Booked hours ÷ Available hours | 85-95% |
| Cancellation rate | Cancelled appointments ÷ Scheduled | Under 10% |
| No-show rate | No-shows ÷ Scheduled | Under 5% |
| Production per hour | Collections ÷ Clinical hours | Context-dependent |
| Production per new patient | First 12 months of revenue per NP | $800-2,000+ |

### Marketing Efficiency
| Metric | What to Extract | Benchmark Range |
|--------|----------------|-----------------|
| Cost per new patient | Marketing spend ÷ New patients | $150-300 (varies by market) |
| Cost per new patient by channel | Channel spend ÷ Channel-attributed NPs | Varies |
| Lifetime patient value | Average annual revenue × Average retention years | $500-1,000/year × years |
| Google review count | Total reviews | Context-dependent |
| Google review rating | Average star rating | 4.5+ |
| Review velocity | New reviews per month | 4+ |

---

## Contradictions to Check

These are common discrepancies in dental practice data. Flag every one you find.

### Financial
- **Production vs. collections gap** — If collections are below 95% of production, where is the money going? Break down: insurance write-offs, patient bad debt, fee schedule issues, timely filing denials
- **P&L totals vs. PMS totals** — Accounting software and practice management software often disagree on revenue. Flag the discrepancy and identify which is source of truth
- **Marketing spend claimed vs. documented** — Owners often forget recurring charges. Check credit card statements against claimed marketing budget
- **Staff cost appears low** — Check if owner or family member compensation is booked differently (draws vs. salary, personal expenses through business)

### Patient Flow
- **New patient count vs. marketing attribution** — If practice claims 30 NPs/month but marketing data only accounts for 15, where are the other 15 coming from? (Referrals? Untracked? Inflated count?)
- **"We're busy" vs. schedule data** — Owners often feel busy when utilization is 70%. Check actual chair utilization against the owner's perception
- **Active patient count vs. actual engagement** — Some PMS counts include patients from 5+ years ago. Verify the 18-month active count, not the total database
- **Recall compliance claimed vs. actual** — "Most of our patients come back" vs. what the recall report actually shows

### Case Acceptance
- **Presented vs. accepted vs. scheduled vs. completed** — These are four different numbers. Many practices only track one or two. A case "accepted" but never scheduled is not accepted
- **Case acceptance rate calculation** — Some software counts by procedure, some by dollar value, some by treatment plan. Clarify which method is being used

### Marketing
- **"We get most patients from referrals"** — This is the most common unverified claim in dental. Check if referral tracking actually exists or if this is a default assumption for untracked patients
- **Google Ads conversions vs. actual new patients** — A form fill or phone call is not a new patient. What's the conversion rate from lead to scheduled to shown to treatment-accepted?
- **Website traffic vs. conversions** — High traffic with low conversion = landing page problem. Low traffic with good conversion = volume problem. The diagnosis depends on which

---

## Common Claims Without Evidence

These are things dental practice owners frequently state as fact but rarely have data to support. Flag them if you hear them and note what data would verify each.

| Common Claim | What Data Would Verify It |
|-------------|--------------------------|
| "We're too busy to take new patients" | Schedule utilization report — if under 90%, this is false |
| "Our case acceptance is pretty good" | Actual case acceptance report from PMS — "pretty good" is not a number |
| "Insurance write-offs are killing us" | Fee schedule analysis vs. UCR rates — quantify the actual impact |
| "We don't need marketing, we get enough referrals" | Referral tracking data + new patient trend over 12 months |
| "Our overhead is in line" | Actual overhead % calculated from P&L — most owners don't know their number |
| "We need more new patients" | Check case acceptance and reactivation first — often the bottleneck is conversion, not volume |
| "Our staff costs are reasonable" | Staff cost as % of collections benchmarked against 25-30% |
| "We lose patients because of insurance changes" | Attrition data broken down by reason — is this the actual top reason or an assumption? |
| "Our hygiene department runs itself" | Hygiene production per hour, perio diagnosis rate, SRP ratio — is hygiene producing or just cleaning? |
| "We tried marketing and it didn't work" | What exactly was tried, for how long, with what budget, measured how? |

---

## Procedure Mix Analysis

When procedure code data is available, categorize production by ADA code category:

| Category | Code Range | What It Tells You |
|----------|-----------|-------------------|
| Diagnostic | D0100-D0999 | Exam/X-ray volume — should be proportional to patient flow |
| Preventive | D1000-D1999 | Hygiene production — prophy, sealants, fluoride |
| Restorative | D2000-D2999 | Bread and butter — fillings, crowns, onlays |
| Endodontics | D3000-D3999 | Root canals — kept in-house or referred out? |
| Periodontics | D4000-D4999 | SRP, perio maintenance — is perio being diagnosed? |
| Prosthodontics | D5000-D5899 | Dentures, partials — aging patient base indicator |
| Implants | D6000-D6199 | Implant production — high-value, kept or referred? |
| Ortho | D8000-D8999 | Ortho/Invisalign — if offered |
| Oral Surgery | D7000-D7999 | Extractions — kept or referred? |

**Key ratios to flag:**
- If restorative is over 60% of production — practice may be over-dependent on insurance-driven work
- If perio codes are under 10% — likely underdiagnosing periodontal disease (national prevalence is ~47% of adults)
- If high-value procedures (implants, ortho, cosmetic) are near zero — revenue ceiling exists
- If diagnostic/preventive is over 40% — practice may not be converting exams into treatment

---

## What This Checklist Does NOT Cover

- Clinical quality of care (this is a business audit, not a clinical audit)
- OSHA/HIPAA compliance
- State dental board regulatory requirements
- Equipment-specific technical assessments
- Staff performance reviews (though staffing costs and ratios are in scope)
- Real estate valuation (though lease terms are in scope for overhead analysis)
