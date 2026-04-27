# brain-template

A Claude Code skill that scaffolds a personal AI knowledge base with automated web scraping. Based on the system Andrej Karpathy described — a `raw/` → `wiki/` → `outputs/` loop that compounds knowledge over time.

## What it does

When invoked, the skill:
1. Asks what topic you want to build a knowledge base for
2. Creates a folder structure (`raw/`, `wiki/`, `outputs/`) in your current directory
3. Writes a `CLAUDE.md` schema file personalized to your topic and interests
4. Optionally scrapes seed URLs into `raw/` using `agent-browser`
5. Prints four reusable starter prompts (scrape, compile wiki, query, health check)

## Requirements

- [Claude Code](https://claude.ai/code)
- Node.js / npm (for `agent-browser`)

## Usage

In Claude Code, run:

```
/llm-knowledge-base [topic]
```

Or omit the topic to be guided interactively.

## How the knowledge base works

```
raw/        ← unmodified source material (scraped or dropped in manually)
wiki/       ← AI-maintained articles, one .md per topic + INDEX.md
outputs/    ← generated reports, answers, and analyses
```

Each wiki article uses `[[topic-name]]` wikilink syntax and starts with a one-paragraph summary. The loop: add sources to `raw/` → compile to `wiki/` → ask questions → save answers back to `outputs/` or update `wiki/` directly.

## Knowledge base skills

Four skills ship with this template for operating your knowledge base after setup:

| Skill | Invoke | What it does |
|-------|--------|--------------|
| `kb-scrape` | `/kb-scrape <url>` | Add any webpage to `raw/` (handles JS-heavy and login-gated pages) |
| `kb-compile-wiki` | `/kb-compile-wiki` | Build or update `wiki/` from everything in `raw/` |
| `kb-query` | `/kb-query <question>` | Ask questions, find gaps, compare sources, generate briefings |
| `kb-health-check` | `/kb-health-check` | Monthly audit for contradictions, unsourced claims, and missing articles |

The compounding loop: `raw/` → `/kb-compile-wiki` → `wiki/` → `/kb-query` → `outputs/` → repeat.

Reusable copies of the prompts that drive these skills are also kept in `references/starter-prompts.md`.
