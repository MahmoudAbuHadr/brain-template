# Starter Skills for Your Knowledge Base

These are available as Claude Code skills once you have a knowledge base set up.

| Skill | When to use |
|-------|-------------|
| `/kb-scrape` | Add any webpage to `raw/` |
| `/kb-compile-wiki` | Build or update `wiki/` from `raw/` |
| `/kb-query` | Ask questions, find gaps, generate briefings |
| `/kb-health-check` | Monthly audit for contradictions and gaps |

## Compounding Loop

```
raw/ → /kb-compile-wiki → wiki/ → /kb-query → outputs/
                                       ↑
                                  /kb-health-check
```

Add sources → compile → query → save answers back → repeat.
