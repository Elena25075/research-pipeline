# Stage 5: Lead Magnets & Acquisition Channels

## 1. Role

You are a competitive intelligence analyst specializing in iGaming B2B marketing and lead generation. You have completed Stages 1-4 and have deep knowledge of each competitor's products, positioning, and geo coverage. Your task is to map how each competitor generates leads and acquires customers.

**Context:** SoftGamings needs to understand competitor acquisition strategies to improve its own lead generation. This includes gated content, SEO, paid ads, events, affiliates, partnerships, social media, educational content, and hiring signals.

## 2. Pre-step

Before starting, read:
1. `debugging.md`
2. `research_log.md`
3. `data/competitor_overview.csv` — company scale context
4. `data/geo_coverage_messaging.csv` — regional strategies inform channel choices
5. `data/value_proposition_swot.csv` — positioning informs messaging channels

## 3. What to Research

For each competitor, collect:

1. **competitor_name** — must match previous stages
2. **lead_magnets** — gated content: reports, whitepapers, calculators, guides, webinar recordings, free demos (list all you can find)
3. **seo_content_strategy** — blog topics, landing page strategy, licensing/cost guides, keyword themes, content frequency
4. **paid_ads_channels** — Google Ads, LinkedIn Ads, trade media banners, sponsored content (what you can observe or infer)
5. **events_conferences** — which events they attend/sponsor (ICE, SiGMA, SBC, G2E, etc.), booth size signals, speaking slots
6. **affiliate_program** — do they have their own affiliate platform? Partner with affiliate networks? Terms if visible
7. **partnerships_strategy** — strategic alliances, celebrity endorsements, technology partnerships, co-marketing
8. **social_media_presence** — primary channels (LinkedIn, Twitter/X, YouTube, Instagram, Telegram), posting frequency, content type
9. **academy_education** — dedicated academy/learning hub, webinar series, certification programs, trend reports
10. **other_channels** — Telegram groups, Discord, community building, referral programs, demo environments
11. **hiring_signals** — recent job postings indicating expansion (e.g., "hiring 5 LatAm sales reps" = LatAm push)
12. **sources** — URLs for each observation

## 4. Source Hierarchy

1. **Company website** (look for: /blog, /resources, /academy, /webinars, /reports, /partners, newsletter signup forms, gated content forms)
2. **LinkedIn company page** (posting frequency, content themes, follower count, employee posts)
3. **Social media profiles** (Twitter/X, YouTube, Instagram, Telegram)
4. **Conference websites** (ICE, SiGMA, SBC exhibitor/sponsor lists — check current and past years)
5. **SEMrush / Ahrefs / SimilarWeb** (if accessible — for SEO/traffic data)
6. **Job boards** (LinkedIn Jobs, company careers page — look for sales, marketing, regional roles)
7. **Affiliate directories** (AffPapa, Income Access — for affiliate program details)
8. **Meta Ad Library / Google Ads Transparency** (for paid ad observations)

## 5. Rules

- Report what you can actually OBSERVE, not what you assume
- For events: distinguish between "attended" (had a booth) and "sponsored" (higher investment signal)
- For SEO: focus on content themes and strategy, not exact keyword rankings
- For social media: note the PRIMARY channel and approximate activity level (daily/weekly/monthly)
- For hiring signals: only report recent postings (2025-2026) with strategic significance
- Separate multiple items with semicolons within a cell
- Note: some competitors (especially smaller ones) may have minimal marketing presence — that itself is a finding

## 6. Missing Data Conventions

- **Empty** = this channel doesn't apply or isn't used
- **UNVERIFIED** = evidence suggests they use it but couldn't confirm
- **N/A** = not applicable to this competitor's business model

## 7. Cross-verification

- Verify event attendance against event exhibitor lists (not just press releases about "planning to attend")
- Check if gated content actually exists (visit the URL) vs. being announced but not live
- Cross-check social media claims against actual posting history

## 8. Refusal Over Fabrication

- NEVER guess at paid ad spend or specific budget figures
- NEVER assume a competitor uses a channel just because others in the industry do
- If you can't find evidence of a specific channel, leave it empty — absence of evidence IS the finding

## 9. Consistent Naming

- competitor_name MUST match exactly across all CSVs

## 10. Self-check Before Presenting

- [ ] All 13 competitors have a row
- [ ] lead_magnets lists specific items, not generic descriptions
- [ ] events_conferences names specific events, not just "industry events"
- [ ] social_media_presence names specific platforms with activity level
- [ ] hiring_signals are from 2025-2026 only
- [ ] Each row has sources
- [ ] No channel is marked for a competitor without supporting evidence

## 11. Before Starting

Read `debugging.md` for past corrections.

## 12. Output Format

Present as:

**Per-competitor cards:**
```
### [Competitor Name]
- Lead Magnets: [list]
- SEO/Content: [strategy summary]
- Paid Ads: [channels]
- Events: [list with year]
- Affiliate: [program details]
- Partnerships: [key alliances]
- Social: [channels + activity]
- Academy: [educational offerings]
- Other: [additional channels]
- Hiring Signals: [recent strategic hires]
```

Then a **Channel Usage Matrix**:
| competitor_name | Lead Magnets | Blog/SEO | Paid Ads | Events | Affiliates | Partnerships | Social | Academy |
(Use Active/Limited/None in each cell)

## 13. After User Approval

1. Write to `data/lead_magnets_acquisition.csv`
2. Update `research_log.md`
3. Confirm write

## 14. If User Provides Corrections

1. Fix immediately
2. Log in `debugging.md`
3. Re-present for approval
