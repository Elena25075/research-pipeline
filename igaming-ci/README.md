# SoftGamings Competitive Intelligence Pipeline

## Start Here

If you're an LLM starting a research session, read these files in order:

1. `prompts/master_system_prompt.md` — your central instructions
2. `debugging.md` — past corrections
3. `research_log.md` — progress tracker
4. `subjects/subject_list.md` — competitor list
5. `research_best_practices.md` — research rules

Then follow the master system prompt: determine session state, report progress, recommend next action, wait for user choice.

## Project Overview

Structured competitive intelligence research for **SoftGamings** — a B2B iGaming platform provider (sportsbook, casino, game aggregator API, licensing). Analyzing 13 competitors across CIS, Asia, Europe, and Latin America to inform product strategy, positioning, lead generation, and regional marketing.

## Pipeline Stages

| Stage | Prompt File | Output CSV(s) | What It Captures |
|-------|------------|---------------|------------------|
| 1 | `prompts/stage1_company_overview.md` | `data/competitor_overview.csv` | Company basics, pricing, client count |
| 2 | `prompts/stage2_products_solutions.md` | `data/products_solutions.csv` | Product portfolio per competitor |
| 3 | `prompts/stage3_licensing_geo.md` | `data/licensing_jurisdictions.csv` + `data/geo_coverage_messaging.csv` | Licenses held, geo presence, regional messaging |
| 4 | `prompts/stage4_value_proposition_swot.md` | `data/value_proposition_swot.csv` | USP, positioning, SWOT vs SoftGamings |
| 5 | `prompts/stage5_lead_magnets_acquisition.md` | `data/lead_magnets_acquisition.csv` | Lead magnets, acquisition channels, hiring signals |
| 6 | `prompts/stage6_media_news.md` | `data/media_news_mentions.csv` | Press coverage, awards, news 2023-2026 |
| 7 | `prompts/stage7_fact_check.md` | All CSVs (corrections) | Cross-verify all data, fix errors |

## Key Rules

1. **Never write to CSV before user approval** — always show data in chat first
2. **UNVERIFIED > guessing** — never fabricate data points
3. **Sources required** — every CSV row must have reference URLs
4. **Consistent naming** — competitor_name must be identical across all CSVs
5. **Sequential stages** — never skip; each stage builds on previous ones

## Project Structure

```
research-pipeline/
├── README.md                          ← you are here (LLM entry point)
├── prompts/
│   ├── master_system_prompt.md        ← central controller
│   ├── stage1_company_overview.md     ← Stage 1 instructions
│   ├── stage2_products_solutions.md   ← Stage 2 instructions
│   ├── stage3_licensing_geo.md        ← Stage 3 instructions
│   ├── stage4_value_proposition_swot.md ← Stage 4 instructions
│   ├── stage5_lead_magnets_acquisition.md ← Stage 5 instructions
│   ├── stage6_media_news.md           ← Stage 6 instructions
│   └── stage7_fact_check.md           ← Stage 7 instructions
├── data/
│   ├── competitor_overview.csv        ← headers only (Stage 1 populates)
│   ├── products_solutions.csv         ← headers only (Stage 2 populates)
│   ├── licensing_jurisdictions.csv    ← headers only (Stage 3 populates)
│   ├── geo_coverage_messaging.csv     ← headers only (Stage 3 populates)
│   ├── value_proposition_swot.csv     ← headers only (Stage 4 populates)
│   ├── lead_magnets_acquisition.csv   ← headers only (Stage 5 populates)
│   └── media_news_mentions.csv        ← headers only (Stage 6 populates)
├── subjects/
│   └── subject_list.md                ← 13 competitors with priorities
├── research_log.md                    ← empty, tracks progress
├── debugging.md                       ← empty, tracks corrections
├── research_best_practices.md         ← iGaming CI research techniques
└── references/
    └── how_to_create_research_pipeline.md ← methodology playbook
```

## Competitors (13 unique)

| # | Competitor | Regions | Priority |
|---|-----------|---------|----------|
| 1 | SOFTSWISS | CIS, Europe, LatAm | High |
| 2 | Slotegrator | CIS, Europe, LatAm | High |
| 3 | BetConstruct | CIS, Asia, LatAm | High |
| 4 | Digitain | CIS, Asia | Medium |
| 5 | NuxGame | CIS | Medium |
| 6 | GamingSoft | Asia | Medium |
| 7 | Uplatform | Asia, LatAm | Medium |
| 8 | GammaStack | Asia | Low |
| 9 | EveryMatrix | Europe | High |
| 10 | ProgressPlay | Europe | Medium |
| 11 | White Hat Gaming | Europe | Medium |
| 12 | Pronet Gaming | Europe | Low |
| 13 | Caleta Gaming | LatAm | Low |
