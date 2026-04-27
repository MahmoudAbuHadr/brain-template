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

## Starter prompts

Four reference prompts are included in `references/starter-prompts.md`:

1. **Scrape a source** — add any webpage to `raw/`
2. **Compile wiki** — build `wiki/` from everything in `raw/`
3. **Ask questions** — query your wiki for gaps, comparisons, briefings
4. **Monthly health check** — find contradictions, unsourced claims, and missing articles
