---
name: kb-compile-wiki
description: Use when raw/ has new or unprocessed sources and the wiki/ needs to be built or updated to reflect them.
---

# Compile Your Wiki

Build or update `wiki/` from everything in `raw/`, following the rules in `CLAUDE.md`.

## Prompt

> Read everything in raw/. Then compile a wiki in wiki/ following the rules
> in CLAUDE.md. Create an INDEX.md first, then create one .md file per major
> topic. Link related topics. Summarize every source.

## Rules (from CLAUDE.md)

- One `.md` file per topic in `wiki/`
- Every article starts with a one-paragraph summary
- Use `[[topic-name]]` wikilink syntax for cross-references
- Maintain `wiki/INDEX.md` — one-line description per topic
- When new sources are added, update relevant existing articles, don't just append

## When to run

After any batch of new files land in `raw/` — whether scraped via `/kb-scrape` or dropped in manually.
