---
name: kb-scrape
description: Use when adding a web article, page, or online source to a knowledge base raw/ folder. Works on JavaScript-heavy pages, login-gated content, and pages requiring scroll or "load more".
---

# Scrape a Web Source

Add any webpage into your knowledge base as a raw markdown file.

## Steps

For each URL:

1. Open the page: `agent-browser open {url}`
2. Wait for content: `agent-browser wait --load networkidle`
3. Extract main content: `agent-browser get text "article"` (fallback: `"main"`, then `"body"`)
4. Get page title: `agent-browser get title`
5. Save to `raw/{slugified-title}.md` with the extracted text
6. Close: `agent-browser close`

## Prerequisites

`agent-browser` must be installed:
```bash
which agent-browser || npm install -g agent-browser && agent-browser install
```

## Notes

- Save to `raw/` only — never modify existing files in `raw/`
- Slugify the title: lowercase, spaces → hyphens, strip special chars
- After scraping, run `/kb-compile-wiki` to fold new sources into the wiki
