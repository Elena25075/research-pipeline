# How to Create a Structured LLM Research Pipeline — Step-by-Step Guide

## Context
Step-by-step guide to create a structured research pipeline for any topic. The output is a self-contained folder that any LLM with file access can pick up and run.

---

## Step 1: Define the Research Scope

Before creating any files, answer these questions:

1. **What is your product?** (e.g., an AI code generation platform for WordPress)
2. **Who is the main audience?** (e.g., WordPress freelancers and agencies building client sites)
3. **What are you researching?** (e.g., competitor pricing, market landscape, feature comparison)
4. **What are the research subjects?** (e.g., 49 competitor tools across 5 categories)
5. **What decisions will this research inform?** (e.g., our own pricing model, feature prioritization)

Write these answers down — they become the context for the master system prompt. The product and audience definitions shape how the LLM interprets competitor data and frames actionable insights.

---

## Step 2: Design the Data Model (CSV Structures)

### 2.1 Identify what data you need to collect

List every data point you want for each research subject. Group them by theme. For the pricing research, the themes were:
- General plan information (prices, tiers, features)
- AI-specific usage details (credits, tokens, limits)
- User perception (quotes, ratings)
- High-level summary (for cross-comparison)

### 2.2 Split into separate CSVs by granularity

Not all data has the same cardinality. Design separate files based on how many rows per subject:

| Pattern | Example | Rows per subject |
|---------|---------|-----------------|
| **1:1** — one row per subject | competitor_summary.csv, voice_of_customer_analysis.csv | 1 |
| **1:many** — multiple rows per subject | plan_tier_details.csv (one per plan), user_sentiment.csv (one per quote) | 3-20 |

Link files with a shared key (e.g., `tool_name` across all CSVs, `plan_name` between plan details and token economics).

### 2.3 Define every column

For each CSV, create a table with:

| Column | Type | Example | Description |
|--------|------|---------|-------------|

**Column naming rules:**
- Use snake_case consistently
- Boolean fields: always `Yes` / `No`
- Missing data: empty = doesn't apply, `UNVERIFIED` = couldn't find, `N/A` = concept doesn't exist
- Prices: always USD
- Dates: YYYY-MM-DD or YYYY-MM

### 2.4 Document relationships

```
summary.csv (1 row per subject)
    ├── detail_a.csv (N rows per subject, linked by subject_name)
    ├── detail_b.csv (N rows per subject, linked by subject_name)
    └── detail_c.csv (1 row per subject, linked by subject_name)
```

---

## Step 3: Design the Research Pipeline

### 3.1 Break research into sequential stages

Each stage should:
- Focus on ONE type of data / ONE CSV
- Be completable in a single LLM session
- Have a clear input (what to research) and output (which CSV to populate)
- Require user approval before writing to CSV

**Order stages so that later stages can use data from earlier ones.** For example:
- Stage 1: Factual data from official sources (pricing, features)
- Stage 2: Detailed technical data (builds on Stage 1 names/structure)
- Stage 3: Quantitative ratings from review platforms
- Stage 4: Qualitative user quotes (uses Stage 3 to know where to look)
- Stage 5: Summary (derives from all previous stages + fills gaps)

### 3.2 Write a prompt for each stage

Each stage prompt should contain these sections (in this order):

```
1. Role — "You are a [role]. You have completed Stages 1-N..."
2. Pre-step — what to read from previous stages before starting
3. What to research — numbered list matching CSV columns exactly
4. Source hierarchy — ordered list of where to look, from most to least reliable
5. Rules — stage-specific constraints
6. Missing data conventions — empty vs UNVERIFIED vs N/A
7. Cross-verification — how to double-check data
8. Refusal over fabrication — explicit "never guess" instructions
9. Consistent naming — naming must match previous stages
10. Self-check before presenting — specific things to verify before showing results
11. Before starting — read debugging.md
12. Output format — exactly how to present results in chat
13. After user approval — what to write and where
14. If user provides corrections — fix, log, re-present
```

**Critical: embed the best practices directly into each prompt.** Do not rely on the LLM remembering to read a separate best practices file — repeat the relevant rules inline.

---

## Step 4: Create Supporting Files

### 4.1 Subject list (e.g., `competitors/competitor_list.md`)

A structured table of all research subjects with:
- Sequential numbering
- Name and website/identifier
- Category grouping
- Priority (High / Medium / Low)
- Notes

Organize by category with clear headers. The LLM reads this to know what to research and in what order.

### 4.2 Research log (`research_log.md`)

Tracks progress per subject per stage:

```markdown
Stage key: 1=[name], 2=[name], 3=[name], ...

| # | Subject | Stage 1 | Stage 2 | ... | Last Updated |
|---|---------|---------|---------|-----|-------------|
```

Start empty. The LLM populates it as research progresses.

### 4.3 Debugging log (`debugging.md`)

Tracks every user correction so mistakes aren't repeated:

```markdown
| # | Date | Subject | Stage | What was wrong | What was correct | Lesson for future |
```

Start empty. The LLM reads this at the start of every session.

### 4.4 Research best practices (`llm_research_best_practices.md`)

A file of research techniques the LLM must apply. Include at minimum:

1. **Prefer refusal over fabrication** — UNVERIFIED > guessing
2. **Source hierarchy** — official sources first, community sources for sentiment only
3. **Cross-verify** — check 2+ sources before reporting facts
4. **Structured output** — data in exact format specified, reasoning in notes column only
5. **Consistent naming** — subject names identical across all CSVs
6. **Handle missing data explicitly** — clear distinction between empty, UNVERIFIED, N/A
7. **Date and currency conventions**
8. **Source-specific rules** (e.g., quote collection rules for sentiment stages)
9. **Self-check checklist** — verify math, booleans, contradictions before presenting
10. **Learning from corrections** — read debugging.md, analyze root cause, log lessons

---

## Step 5: Write the Master System Prompt

This is the central controller. It must contain:

### 5.1 Role definition
One paragraph explaining who the LLM is and what the project is about.

### 5.2 Session startup sequence
Ordered list of files to read before doing any work:
1. debugging.md
2. research_log.md
3. subject list
4. best practices

### 5.3 Session state detection
Instructions for the LLM to:
- Check what's been completed
- Find any in-progress subjects
- Recommend what to do next
- Ask the user which subject to research

### 5.4 Pipeline flow
For each stage: which prompt to load, what to present, when to wait for approval, what to write on approval, what to do on correction.

### 5.5 Correction handling
Step-by-step: fix → analyze root cause → log in debugging.md → re-present.

### 5.6 Output rules
Boolean format, UNVERIFIED convention, currency, dates, show-before-write rule.

### 5.7 Session ending
Update research_log.md, add session history entry, note resume point.

### 5.8 What NOT to do
Explicit prohibitions: no fabrication, no skipping stages, no writing before approval, no per-subject report files.

---

## Step 6: Create the README

The README serves as the universal entry point for any LLM. It must contain:

1. **"Start Here" section** — ordered reading list pointing to master prompt and supporting files
2. **Project overview** — one paragraph on what this research is about
3. **Pipeline stages table** — stage number, prompt file, output CSV, what it captures
4. **Key rules** — the 5 most important rules in bullet form
5. **Project structure** — ASCII tree of all files and folders

---

## Step 7: Create the Startup Prompt

Write a short prompt the user can copy-paste into any LLM to begin a session:

```
You are a [role] research assistant. Your project folder is at [PATH].

Read these files in order before doing anything:
1. README.md
2. prompts/master_system_prompt.md
3. debugging.md
4. research_log.md
5. [subject_list].md
6. [best_practices].md

After reading, follow the master system prompt: determine session state,
show progress summary, recommend next subject. Wait for my choice.

Do not skip any files. Do not start research until you have read all of the above.
```

---

## Step 8: Assemble the Folder Structure

```
project_name/
├── README.md                          ← universal entry point
├── prompts/
│   ├── master_system_prompt.md        ← LLM reads this first
│   ├── stage1_[name].md
│   ├── stage2_[name].md
│   ├── stage3_[name].md
│   ├── stage4_[name].md
│   └── stage5_[name].md              ← (or however many stages you need)
├── data/
│   ├── [csv_1].csv                    ← headers only, no data
│   ├── [csv_2].csv
│   ├── [csv_3].csv
│   └── ...
├── subjects/
│   └── subject_list.md                ← all research subjects with priorities
├── research_log.md                    ← empty, ready for use
├── debugging.md                       ← empty, ready for use
└── research_best_practices.md         ← techniques for accurate research
```

**All CSVs start with headers only — no data.** The LLM populates them through the pipeline.

---

## Step 9: Quality Checklist Before Packing

Before sending the folder to another machine, verify:

- [ ] Every CSV column mentioned in a stage prompt exists in the actual CSV header
- [ ] Column names are identical between CSV headers and stage prompts (exact spelling, snake_case)
- [ ] Stage prompts reference the correct stage numbers (if you reordered stages, check all cross-references)
- [ ] The master system prompt's pipeline flow matches the actual stage prompt filenames
- [ ] Subject list has no UNVERIFIED websites (delete or verify before packing)
- [ ] research_log.md is empty (no leftover data from testing)
- [ ] debugging.md is empty (no leftover data from testing)
- [ ] All CSVs contain headers only (no leftover data)
- [ ] No legacy/orphan files remain in the folder
- [ ] README project structure matches the actual file listing
- [ ] Startup prompt references correct file paths
- [ ] All stage prompts embed the relevant best practices inline (don't rely on the LLM reading the best practices file during research)

---

## Common Mistakes to Avoid

1. **Stage prompts out of sync with CSV columns** — after renaming or merging columns, always update both the CSV header AND every stage prompt that references those columns
2. **Inconsistent stage numbering** — if you swap stage order, search for ALL references to "Stage 3", "Stage 4", "Stages 1-2", "Stages 1-3" etc. across every file
3. **Best practices not embedded in prompts** — the LLM may not read the best practices file during research. Embed the critical rules directly in each stage prompt.
4. **Missing cross-references between stages** — later stages should reference what to read from earlier stages (e.g., "Read Stage 3 VoC data to know which platforms have reviews")
5. **No self-check section** — every stage prompt should have a "verify before presenting" checklist specific to that stage's data type
6. **Overly wide CSVs** — if a CSV has 20+ columns, tell the stage prompt to split output into multiple grouped tables
7. **No correction loop** — every stage prompt must include: fix → log in debugging.md → re-present for approval

---

## Adapting for Different Research Topics

To use this framework for a different topic, change:

1. **Step 1:** Research scope and goals
2. **Step 2:** CSV columns (the data you're collecting)
3. **Step 3:** Number and focus of stages (you may need 3 stages or 7 — adapt to your data)
4. **Step 4:** Subject list content, source hierarchy in best practices
5. **Step 5:** Role definition and project context in master prompt
6. **Steps 6-7:** Update README and startup prompt to match

The structural patterns — pipeline flow, approval gates, debugging loop, naming conventions, missing data handling — remain the same regardless of topic.
