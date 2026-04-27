---
name: kb-query
description: Use when asking questions, finding knowledge gaps, comparing sources, or generating briefings from a compiled wiki/. Requires wiki/ to have 10+ articles.
---

# Query Your Wiki

Ask questions against your knowledge base and save answers back to keep the system compounding.

## Starter Prompts

**Find gaps:**
> Based on everything in wiki/, what are the three biggest gaps in my understanding of [topic]?

**Compare sources:**
> Compare what source A says about [concept] vs what source B says. Where do they disagree?

**Generate a briefing:**
> Write me a 500-word briefing on [topic] using only what's in this knowledge base.

## Compounding Loop

Save answers back into `outputs/` or update `wiki/` articles directly. Every query makes the system smarter.

## Prerequisites

Run `/kb-compile-wiki` first if `wiki/` is empty or stale.
