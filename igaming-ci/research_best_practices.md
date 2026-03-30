# iGaming Competitive Intelligence — Research Best Practices

## 1. Prefer Refusal Over Fabrication

Never guess. If you can't find a data point from a credible source, mark it UNVERIFIED. This applies especially to:
- Revenue figures (most iGaming B2B companies are private)
- Pricing (rarely published publicly)
- Exact client counts
- License numbers

UNVERIFIED is always better than a wrong number that drives bad strategy.

## 2. Source Hierarchy for iGaming B2B

**Tier 1 — Primary Sources (highest trust):**
- Official company website (product pages, about, pricing)
- Regulatory databases (MGA public register, UKGC license search, PAGCOR)
- Financial filings (for public companies: Evolution, Flutter, DraftKings)

**Tier 2 — Industry Intelligence:**
- Trade press: iGB, SBC News, Gambling Insider, Yogonet, European Gaming, EEGaming
- Conference presentations: ICE Barcelona, SiGMA, SBC Summit, G2E
- Annual reports: SOFTSWISS iGaming Trends Report, Famesters Report

**Tier 3 — Third-party Data:**
- Crunchbase, Tracxn, PitchBook (funding, revenue estimates, employee count)
- LinkedIn (employee count proxy, hiring signals)
- SimilarWeb, SEMrush (traffic, SEO data)

**Tier 4 — Community/Review Sources (use for sentiment only):**
- Trustpilot, G2, AskGamblers (player/operator reviews)
- Glassdoor (internal culture signals)
- Reddit, forums (unverified but can surface real issues)

## 3. Cross-Verify Key Claims

Before reporting a fact, check it against 2+ sources:
- Employee count: LinkedIn vs. Crunchbase/Tracxn
- Revenue: multiple estimation sources (ZoomInfo, Craft.co, Tracxn)
- License status: official regulatory database vs. company claims
- Game count: company claims vs. aggregator databases

If sources conflict, report the range and note the discrepancy.

## 4. iGaming-Specific Data Rules

- **Prices:** Always in USD. Convert from EUR at current rate, noting the conversion
- **Dates:** YYYY-MM-DD or YYYY-MM format
- **Booleans:** Yes / No (not True/False, not Y/N)
- **Game counts:** Change frequently — always note the date of the count
- **Revenue share:** Distinguish between NGR (Net Gaming Revenue) and GGR (Gross Gaming Revenue) — these are different bases
- **License numbers:** Format varies by regulator. MGA: MGA/B2B/xxx/yyyy. UKGC: 5-digit number

## 5. Missing Data Conventions

| Notation | Meaning | Example |
|----------|---------|---------|
| Empty cell | Doesn't apply to this competitor | Payment gateway game_count |
| UNVERIFIED | Searched but couldn't find reliable data | Revenue for a private company |
| N/A | Concept doesn't exist for this competitor | Setup fee for a content-only supplier |

## 6. Consistent Naming

- Use EXACT competitor names from `subjects/subject_list.md` across ALL CSVs
- These are the primary keys that link all data together
- Never abbreviate (BC ≠ BetConstruct) or change case (SoftSwiss ≠ SOFTSWISS)

## 7. iGaming Lead Magnet & Marketing Intelligence

When researching acquisition channels:
- Check for gated content: look for email capture forms, PDF downloads, "Get the report" CTAs
- Check blog post frequency and topics (licensing guides, cost calculators, market reports are common lead magnets)
- Conference presence signals budget: platinum sponsor > gold > exhibitor > attendee
- LinkedIn is the #1 B2B channel in European/NA iGaming; Instagram/Telegram dominate in Asia/LatAm
- Job postings are leading indicators: "Hiring LatAm Sales Manager" = LatAm expansion in 6-12 months

## 8. Media Monitoring Rules

- Cover 2023-2026 for a complete picture
- Prioritize: M&A, license grants, product launches, partnerships, awards, regulatory actions
- Skip routine press releases ("Company X to attend Event Y")
- For negative news (fines, breaches): verify against regulatory body's official notice
- Sentiment must be honest: a UKGC fine is "negative" even if the company's press release spins it positively

## 9. SWOT Analysis Rules

- Every SWOT claim must reference specific facts from earlier stages
- Bad: "Strong platform." Good: "40K+ games via single API — 2x SoftGamings' aggregator"
- Every competitor has BOTH strengths AND weaknesses — no one is all-good or all-bad
- Opportunities should be actionable — things SoftGamings can DO, not just observations
- Threats should be specific — "growing in LatAm" is vague; "certified in Brazil with 81% GGR growth" is specific

## 10. Self-Check Before Every Presentation

Before showing any data to the user:
- [ ] Competitor names match exactly across all CSVs
- [ ] No empty rows (every competitor has data)
- [ ] Sources column populated for every row
- [ ] Numbers pass sanity checks (revenue vs. employee count, game count vs. industry norms)
- [ ] No contradictions between CSVs
- [ ] UNVERIFIED used honestly (not to hide lazy research)
- [ ] Dates within expected ranges
- [ ] Categories/types use only the defined allowed values
