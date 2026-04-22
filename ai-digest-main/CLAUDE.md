# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this project is

A static blog/digest site built with **Astro 6 (SSG)**, deployed to Vercel. The theme is freediving, breath techniques, and hypoxia training. Content lives in `src/content/blog/` as Markdown/MDX files. No CMS — articles are authored or generated directly as `.md` files.

## Commands

```bash
npm run dev       # dev server → http://localhost:4321
npm run build     # production build → dist/
npm run preview   # serve dist/ locally
```

Node ≥ 22.12.0 required.

## Architecture

**Content flow:**
1. `.md` / `.mdx` files in `src/content/blog/` — frontmatter validated by Zod schema in `src/content.config.ts`
2. `src/pages/blog/index.astro` — lists all posts sorted by `pubDate` descending
3. `src/pages/blog/[...slug].astro` — generates one static page per post via `getStaticPaths()`
4. `src/pages/rss.xml.js` — RSS feed from the same collection

**Key constants:** `src/consts.ts` holds `SITE_TITLE` and `SITE_DESCRIPTION`.

**Site URL** is set in `astro.config.mjs` — currently `https://example.com`, must be updated before deploying.

## Blog post frontmatter schema

```yaml
---
title: 'Article Title'           # required
description: 'Two-three sentences'  # required
pubDate: '2026-03-25'            # required, ISO date
updatedDate: '2026-03-26'        # optional
heroImage: placeholder-cover.jpg  # optional, relative to public/
source: 'https://...'            # optional, original article URL
tags: ['freediving', 'apnea']    # default []
---
```

## Styling

Plain CSS only — no Tailwind. Design tokens (accent color, grays, shadows) are CSS variables in `src/styles/global.css`. Mobile breakpoint at 720px.
