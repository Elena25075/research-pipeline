# research-pipeline

Creates a self-contained LLM research pipeline project for structured research on any topic.

## What It Does

Guides you through designing and building a complete research pipeline — CSV data models, stage-by-stage LLM prompts, supporting files, and a README entry point. The output is a portable folder that any LLM with file access can pick up and run to systematically research dozens of subjects.

## Who It's For

Product managers, founders, and researchers who need to systematically analyze many subjects (competitors, tools, markets) and want structured, verifiable data — not a wall of prose.

## Usage

```
/research-pipeline
```

The skill walks you through 9 phases interactively. You provide the research topic and data requirements; it generates the entire project infrastructure.

## Workflow

```
Phase 1: Define research scope (product, audience, topic, subjects)
    ↓
Phase 2: Design CSV data model (columns, types, relationships)
    ↓
Phase 3: Design pipeline stages (order, dependencies, sources)
    ↓
Phase 4: Write stage prompts (14-section format with embedded best practices)
    ↓
Phase 5: Create supporting files (subject list, logs, best practices)
    ↓
Phase 6: Write master system prompt (central controller)
    ↓
Phase 7: Create README (universal LLM entry point)
    ↓
Phase 8: Generate startup prompt (copy-pasteable for any LLM)
    ↓
Phase 9: Quality check (verify consistency across all files)
```

## Output

A complete project folder:

```
project_name/
├── README.md                      ← any LLM starts here
├── prompts/                       ← stage-by-stage research instructions
├── data/                          ← CSV files (headers only, LLM populates)
├── subjects/                      ← research subjects with priorities
├── research_log.md                ← progress tracker
├── debugging.md                   ← correction log
└── research_best_practices.md     ← research techniques
```

## Key Principles

- Structure before research — build the pipeline completely before starting any analysis
- User approves everything — no files written without explicit approval
- Prompts are self-contained — each stage prompt has all rules inline
- CSVs are the single source of truth — no duplicate data in reports
- Portable by design — works on any machine, with any LLM

## When NOT to Use

- One-off research questions (just ask the LLM directly)
- Research with fewer than 5 subjects (overkill for small sets)
- When you don't need structured, comparable data across subjects
- When you want prose reports instead of tabular data

## Related Skills

- `/ideate` - Use before this skill to validate whether the research is worth doing
- `/create-plan` - Use after this skill if you need an implementation plan based on findings

## License

MIT
