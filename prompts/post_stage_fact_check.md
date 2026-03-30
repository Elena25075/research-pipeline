# Post-Stage Fact-Check Protocol

This protocol runs AFTER every research stage (not just Stage 7). Every data point written to a CSV must pass this verification before the stage is marked complete.

---

## Fact-Check Framework: SIFT + CRAAP Adapted for iGaming CI

### SIFT Method (for each claim)
1. **Stop** — Don't accept the first result. Pause before recording
2. **Investigate the source** — Is this an official page, trade press, or user-generated?
3. **Find better coverage** — Can you find the same claim from an independent source?
4. **Trace the claim** — Where did this number originate? Marketing copy ≠ verified fact

### CRAAP Test (for each source)
- **Currency** — Is the data from 2024-2026? Older = flag for re-verification
- **Relevance** — Does the source actually address this specific data point?
- **Authority** — Official site > trade press > review site > forum
- **Accuracy** — Can the claim be verified against a primary database?
- **Purpose** — Is the source marketing (biased) or editorial/regulatory (more objective)?

---

## Source Reliability Tiers

| Tier | Source Type | Trust Level | Use For |
|------|-----------|-------------|---------|
| **S** | Regulatory databases (MGA, UKGC, PAGCOR registers) | Verified fact | License numbers, license status, enforcement actions |
| **S** | Corporate registries (Malta MFSA, UK Companies House) | Verified fact | Founded year, HQ, legal entity, directors |
| **A** | Official company website | High (but biased) | Products, pricing, team, stated client count |
| **A** | Financial filings (public companies only) | Verified fact | Revenue, employee count, M&A |
| **B** | Trade press (iGB, SBC News, Gambling Insider, Yogonet) | High | News, partnerships, product launches, interviews |
| **B** | Crunchbase / PitchBook / Tracxn | Medium-High | Funding, revenue estimates, employee count |
| **C** | LinkedIn | Medium | Employee count proxy, hiring signals, office locations |
| **C** | Review sites (iGamingX, WhiteLabelWonder, G2) | Medium | Product descriptions, comparative analysis |
| **D** | ZoomInfo / Craft.co / Growjo | Low-Medium | Revenue estimates (wide ranges, often inaccurate) |
| **D** | Trustpilot / Glassdoor | Low (subjective) | Sentiment only, not facts |
| **F** | Forums, Reddit, unattributed blogs | Unreliable | Never use for factual claims |

---

## Verification Checklist by Data Type

### Company Basics (founded, HQ, CEO)
- [ ] **Founded year**: Cross-check official About page vs. Crunchbase vs. corporate registry
- [ ] **HQ location**: Verify against corporate registry (Malta MFSA for MGA-licensed companies, UK Companies House for UK entities)
- [ ] **CEO/leadership**: Check official website team page + LinkedIn profile
- [ ] **Action if conflict**: Use corporate registry as ground truth; note discrepancy

### Employee Count
- [ ] Check LinkedIn company page ("X employees on LinkedIn")
- [ ] Cross-reference with Crunchbase/Tracxn
- [ ] If >50% discrepancy between sources, report range and mark confidence as LOW
- [ ] **Red flag**: Marketing claim of "500+ staff" but LinkedIn shows 80 profiles = investigate

### Revenue Estimates
- [ ] For public companies: use financial filings (ground truth)
- [ ] For private companies: cross-check Tracxn vs. ZoomInfo vs. Craft.co
- [ ] If estimates vary by >3x across sources, mark UNVERIFIED
- [ ] **Never** report a single source revenue estimate as fact — always prefix with "~"
- [ ] **Red flag**: Revenue claims from company marketing without third-party corroboration

### Pricing
- [ ] Is this from an official pricing page? (rare in iGaming B2B)
- [ ] Is this from a credible review site citing specific deal terms?
- [ ] Is this an industry-standard range estimate? If so, label as "(est.)"
- [ ] **Default**: Mark as UNVERIFIED unless from official source or named case study
- [ ] **Never** present estimated pricing as confirmed pricing

### Client Count & Notable Clients
- [ ] Client count: from official website or press release?
- [ ] Notable clients: independently verifiable? (press release from BOTH parties, or regulatory filing)
- [ ] **Red flag**: "1000+ clients" claim with zero named clients = treat with skepticism
- [ ] Cross-check named clients against the client's own website (do they mention using this platform?)

### License Verification (iGaming-specific)
- [ ] **MGA**: Search https://www.mga.org.mt/licensee-register/ — verify license number and status
- [ ] **UKGC**: Search https://www.gamblingcommission.gov.uk/public-register — verify account number
- [ ] **Curacao**: Check if specific license number is cited (old Curacao sublicenses are being phased out)
- [ ] **PAGCOR**: Check accredited operator list on PAGCOR website
- [ ] **Action**: If company claims a license but it's not in the public register, mark UNVERIFIED

### Game/Provider Counts
- [ ] Cross-check company claim against aggregator databases or review sites
- [ ] Note the date of the count (these change monthly)
- [ ] **Red flag**: Round numbers (exactly "10,000 games") are usually marketing approximations
- [ ] Accept ranges: "16,000-16,500" is more honest than "16,500"

---

## Post-Stage Fact-Check Process (run after EVERY stage)

### Step 1: Automated Consistency Checks
For the stage just completed:
- [ ] All competitor_name values match `subjects/subject_list.md` exactly
- [ ] No duplicate rows (same competitor + same key data)
- [ ] All required fields populated (not blank where data should exist)
- [ ] Enum fields use only allowed values (categories, types, regions)
- [ ] Dates in correct format (YYYY-MM or YYYY-MM-DD)
- [ ] Numbers pass sanity check (no negative values, no impossible ranges)

### Step 2: Source Audit
For each row in the stage's CSV(s):
- [ ] Sources column is populated with at least 1 URL
- [ ] Rate each source against the reliability tier table above
- [ ] Flag any row where ALL sources are Tier D or lower
- [ ] Flag any row with zero sources → must add source or mark UNVERIFIED

### Step 3: Cross-Verification Spot Checks
Select 3-5 high-impact claims per competitor and verify:
- [ ] Visit the source URL — does it still load?
- [ ] Does the source actually support the specific claim?
- [ ] Can you find the same claim from an independent second source?
- [ ] Is the source current (not >2 years old for fast-changing data)?

Priority claims to spot-check:
1. Revenue/financial figures
2. License numbers
3. Client counts
4. Game/provider counts
5. Pricing data

### Step 4: Assumption Detection
Scan for language patterns that indicate assumptions:
- "likely", "probably", "estimated", "typical", "usually" → flag as assumption
- Round numbers without source → flag for verification
- Industry-standard ranges applied to a specific company → flag as estimate
- Marketing copy taken verbatim → flag as unverified self-report

### Step 5: Correction & Documentation
For every issue found:
1. **Fix** the data point (correct value or change to UNVERIFIED)
2. **Log** in `debugging.md`: date, competitor, field, what was wrong, what was corrected
3. **Tag** each correction with severity:
   - **CRITICAL**: Wrong fact that would cause bad strategy (wrong revenue, wrong license)
   - **MODERATE**: Imprecise data (employee range too wide, outdated game count)
   - **MINOR**: Formatting, consistency, or style issues

### Step 6: Fact-Check Summary
Present to user:
```
Stage [X] Fact-Check Results:
- Data points checked: [N]
- Issues found: [N] (Critical: X, Moderate: X, Minor: X)
- Corrections applied: [N]
- Items changed to UNVERIFIED: [N]
- Confidence score: HIGH / MEDIUM / LOW
```

---

## Confidence Scoring Per Row

After fact-checking, mentally assign each row a confidence level:

| Confidence | Criteria |
|-----------|---------|
| **HIGH** | 2+ independent Tier A/B sources confirm; no conflicting data |
| **MEDIUM** | 1 Tier A/B source + consistent with other data; minor gaps |
| **LOW** | Single Tier C/D source only; or conflicting sources; or significant UNVERIFIED fields |
| **UNVERIFIED** | No credible source found; data is a placeholder or assumption |

---

## iGaming-Specific Verification Databases

| Database | URL | What to Verify |
|----------|-----|---------------|
| MGA Licensee Register | mga.org.mt/licensee-register/ | Malta gambling licenses |
| UKGC Public Register | gamblingcommission.gov.uk/public-register | UK gambling licenses |
| Malta MFSA Company Registry | registry.mfsa.mt | Company incorporation, directors |
| UK Companies House | find-and-update.company-information.service.gov.uk | UK company details |
| Curacao Gaming Authority | curacao-gaming.com | Curacao license verification |
| PAGCOR | pagcor.ph | Philippines accreditation |
| LinkedIn Company Search | linkedin.com/company/ | Employee count, office locations |
| Crunchbase | crunchbase.com | Funding, founding, leadership |
| Tracxn | tracxn.com | Revenue estimates, competitor ranking |
