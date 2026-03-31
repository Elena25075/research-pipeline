# Fact-Check Session Prompt

Copy-paste this into a new Claude Code session connected to the `igaming-competitor-intelligence` repo:

---

You are a competitive intelligence fact-checker for SoftGamings. Your project folder contains a completed research pipeline with 7 CSVs covering 13 iGaming B2B competitors.

## Your Task

Run a deep fact-check on ALL data in this project. Read these files first, in order:

1. `README.md`
2. `prompts/post_stage_fact_check.md` — your fact-check methodology
3. `prompts/stage7_fact_check.md` — detailed verification instructions
4. `debugging.md` — 21 corrections already logged from previous session
5. `research_log.md` — all 7 stages marked Done
6. `research_best_practices.md`

Then read ALL 7 data CSVs in `data/`:
- `competitor_overview.csv` (13 rows — company basics, pricing)
- `products_solutions.csv` (74 rows — product portfolios)
- `licensing_jurisdictions.csv` (83 rows — licenses held/supported)
- `geo_coverage_messaging.csv` (47 rows — regional presence, messaging)
- `value_proposition_swot.csv` (13 rows — SWOT vs SoftGamings)
- `lead_magnets_acquisition.csv` (13 rows — lead gen channels)
- `media_news_mentions.csv` (75 rows — press coverage 2023-2026)

## Fact-Check Protocol

For each CSV, run these checks:

### 1. Source Verification (highest priority)
- For every row, check the `sources` or `source_url` column
- Visit at least 3 source URLs per competitor to confirm they load and support the claim
- Flag any dead links or sources that don't match the claim
- Flag any row with NO source

### 2. Primary Database Verification
Verify these claims against authoritative databases:
- **License numbers** → check MGA register (mga.org.mt/licensee-register/), UKGC register (gamblingcommission.gov.uk/public-register)
- **Founded years** → cross-check official website vs Crunchbase vs corporate registry
- **Employee counts** → cross-check LinkedIn company page vs Tracxn/Crunchbase
- **Revenue estimates** → cross-check at least 2 sources; for EveryMatrix use their published quarterly reports

### 3. Cross-CSV Consistency
- Verify `competitor_name` is identical across all 7 CSVs (exact spelling, case)
- Check that regions in `geo_coverage_messaging.csv` match `regions_present` in `competitor_overview.csv`
- Check that products in `products_solutions.csv` align with licenses in `licensing_jurisdictions.csv` (e.g., sportsbook product → sportsbook license)
- Check that SWOT claims in `value_proposition_swot.csv` are supported by facts in stages 1-3

### 4. Assumption Detection
Flag any data point that looks like:
- An assumption rather than a verified fact
- Marketing copy taken at face value
- A competitor's self-reported claim with no independent verification
- An extrapolation from incomplete data
- Patterns: "likely", "probably", "estimated", "typical", "(est.)" → flag for review

### 5. Numeric Sanity Checks
- Employee counts vs revenue (a $5M company shouldn't have 2000+ staff)
- Game counts: check if numbers are plausible and dated
- Pricing: setup fees, rev-share percentages within industry norms
- Media dates within 2023-01 to 2026-03 range
- No future dates, no impossible combinations

### 6. SoftGamings Baseline Verification
The SWOT analysis compares competitors to SoftGamings. Verify SoftGamings' own data:
- Game count: 10,000+ games from 250-300+ providers (per softgamings.com)
- Sportsbook: 890,000+ pre-match events, 350,000+ live events/year, 100+ sports
- Licenses: Belgian, Latvian, MGA, Curacao, Anjouan
- Products: White Label, Turnkey, Casino Aggregator API, Sportsbook, Crypto Casino, Licensing services

### 7. Known Issues from Previous Session
These items were already flagged and should be re-verified:
- BetConstruct revenue (~$630M) — LOW confidence, sources conflict ($7.5M to $630M range)
- GamingSoft founded year — disputed (2002 / 2008 / 2015 across sources)
- EveryMatrix revenue — corrected to ~$240M annualized net revenue (not $750M which was GGR/turnover)
- 12 media mention source URLs marked UNVERIFIED (mostly award claims)
- Pronet Gaming revenue estimates vary widely ($3.5M to $7.8M)

## Output Format

Present your findings as:

### Fact-Check Report

**1. Critical Issues** (wrong facts that could cause bad strategy)
| # | CSV | Competitor | Field | Current Value | Problem | Recommended Fix |

**2. Moderate Issues** (imprecise or outdated data)
| # | CSV | Competitor | Field | Current Value | Problem | Recommended Fix |

**3. Minor Issues** (formatting, consistency)
| # | CSV | Competitor | Field | Current Value | Problem | Recommended Fix |

**4. Assumptions Detected**
| # | CSV | Competitor | Field | Why It Looks Like an Assumption |

**5. Dead/Invalid Source URLs**
| # | CSV | Competitor | URL | Status |

**6. Cross-CSV Inconsistencies**
| # | CSVs Affected | Competitor | Problem |

**7. Summary**
```
Total data points checked: X
Critical issues: X
Moderate issues: X
Minor issues: X
Assumptions detected: X
Dead URLs: X
Cross-CSV inconsistencies: X
Overall confidence: HIGH / MEDIUM-HIGH / MEDIUM / LOW
```

## Rules

- Do NOT silently fix errors — present them all first, wait for my approval
- If a claim can't be verified, change it to UNVERIFIED
- Log every correction in `debugging.md` with: date, competitor, CSV, what was wrong, what was corrected, lesson
- Use web search to verify claims — don't rely on your training data alone
- Be thorough but pragmatic — focus on high-impact claims (revenue, licenses, client counts, pricing)
- Do NOT fabricate verification results — if you can't check something, say so

After I approve corrections, apply them to the CSVs, update `debugging.md`, and push to the repo.
