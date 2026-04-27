# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Repository Is

A Claude skill template (`llm-knowledge-base`) that scaffolds a personal AI knowledge base with automated web scraping. When invoked as a skill, it guides the user through creating a topic-scoped folder structure, a schema file, and optionally scraping seed URLs using `agent-browser`.

The repository has no build system, tests, or application code — it is pure procedural documentation executed by Claude.

## Repository Structure

- `.claude/skills/llm-knowledge-base/SKILL.md` — The skill definition. Claude reads and executes this as a 6-step workflow when the skill is invoked.
- `references/starter-prompts.md` — Four reusable prompts printed at the end of setup for the user to copy. Referenced in SKILL.md as `${CLAUDE_SKILL_DIR}/references/starter-prompts.md`.

## Skill Workflow (SKILL.md)

The skill runs in the **user's working directory**, not this repo. Steps:

1. **Check dependencies** — verify `agent-browser` is installed globally (`npm install -g agent-browser && agent-browser install`); install the agent-browser skill via `npx skills add` if missing.
2. **Determine topic** — use `$ARGUMENTS` if provided (slugified), otherwise ask the user three questions interactively.
3. **Scaffold folders** — `mkdir -p {topic-slug}/raw {topic-slug}/wiki {topic-slug}/outputs`
4. **Write schema** — create `{topic-slug}/CLAUDE.md` from the template in SKILL.md, personalized with the user's topic and interests.
5. **Scrape seed URLs** — if the user provided URLs, use `agent-browser` to extract and save content into `raw/`.
6. **Print starter prompts** — read and print `references/starter-prompts.md` listing the four skills.

## agent-browser Integration

`agent-browser` is an external npm tool for scraping JS-heavy pages. The scraping pattern in SKILL.md is:
```bash
agent-browser open {url}
agent-browser wait --load networkidle
agent-browser get text "article"   # fallback: "main", then "body"
agent-browser get title
agent-browser close
```
Extracted content is saved as markdown in `{topic-slug}/raw/{slugified-title}.md`.

## Knowledge Base Skills

Four skills ship with this repo for operating a knowledge base after setup:

| Skill | Invoke | When to use |
|-------|--------|-------------|
| kb-scrape | `/kb-scrape` | Add any webpage to `raw/` |
| kb-compile-wiki | `/kb-compile-wiki` | Build or update `wiki/` from `raw/` |
| kb-query | `/kb-query` | Ask questions, find gaps, generate briefings |
| kb-health-check | `/kb-health-check` | Monthly audit for contradictions and gaps |

The compounding loop: `raw/` → `/kb-compile-wiki` → `wiki/` → `/kb-query` → `outputs/` → repeat.

## Knowledge Base Schema Convention

Each scaffolded knowledge base uses this three-folder convention:
- `raw/` — unmodified source material (never edit)
- `wiki/` — AI-maintained articles, one `.md` per topic, with `INDEX.md`
- `outputs/` — generated reports and query answers

Wiki articles use `[[topic-name]]` wikilink syntax and must start with a one-paragraph summary.
