---
name: kb-health-check
description: Use when doing a periodic review of wiki/ to surface contradictions, unsourced claims, unexplained topics, and article gaps. Run monthly.
---

# Monthly Health Check

Audit your entire wiki for quality issues and gaps.

## Prompt

> Review the entire wiki/ directory. Flag any contradictions between
> articles. Find topics mentioned but never explained. List any claims
> that aren't backed by a source in raw/. Suggest 3 new articles that
> would fill gaps.

## What it surfaces

| Issue | Description |
|-------|-------------|
| Contradictions | Articles that disagree with each other |
| Orphaned mentions | Topics referenced via `[[wikilink]]` with no article |
| Unsourced claims | Assertions with no matching file in `raw/` |
| Gap suggestions | 3 new articles that would strengthen the knowledge base |

## Cadence

Run once a month, or after a large batch of scraping.
