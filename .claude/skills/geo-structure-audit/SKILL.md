---
name: geo-structure-audit
description: Comprehensive audit of a webpage's structure, content freshness, schema, and metadata to assess AI extractability and GEO readiness.
allowed-tools: [WebFetch, Read, Bash, AskUserQuestion]
---

# GEO Structure & Extractability Audit (Enhanced)

## Purpose
Perform a deep analysis of a webpage to determine how easily AI engines (like ChatGPT Search, Perplexity, Google SGE) can extract, understand, and cite its content. This audit goes beyond basic headings to include sitemap health, freshness signals, structured data, and technical rendering.

## Instructions

When the user provides a URL, follow these steps in order. Use the page's HTML and HTTP headers (from `WebFetch`). If the site has multiple pages, you may need to fetch additional URLs (e.g., sitemap.xml, about page) as indicated.

### Step 1: Fetch the page and extract metadata
- Get the URL using `WebFetch`, capturing status, headers, and HTML.
- Record:
  - HTTP status (200, 301, etc.)
  - `Last-Modified` header (if present) – indicates freshness.
  - `Content-Type` – ensure it's HTML.
- From HTML, extract:
  - `<title>` – quality check: descriptive, under 60 chars.
  - `<meta name="description">` – present? under 160 chars? engaging?
  - `<meta property="og:..."` and `<meta name="twitter:..."` – presence and completeness.
- **Output:** status, last-modified, title, description, social tags.

### Step 2: Analyze sitemap and site structure
- Attempt to fetch `/sitemap.xml` (or `/sitemap_index.xml`). If found, parse it to list all URLs.
- Identify which important page types are present: homepage, about, services/products, blog, contact, etc.
- If sitemap missing, note that as a weakness.
- **Output:** list of sitemap URLs, coverage assessment (e.g., "only homepage listed").

### Step 3: Check content rendering (server-side vs client-side)
- Inspect the HTML for large amounts of JavaScript and minimal text. If the visible content is not in the raw HTML (e.g., Divi, React without SSR), flag as "JS‑heavy – content may be invisible to crawlers."
- Look for `<div>`s with content – if most text is inside script tags or dynamically loaded, note the risk.
- **Output:** rendering verdict (Server‑rendered / Client‑side / Mixed).

### Step 4: Evaluate heading structure
- Extract all H1–H6 tags.
- Count H1s (should be exactly one). If multiple, flag.
- List H2s and assess if they represent distinct subtopics (avoid generic ones like "Why Choose Us").
- **Output:** heading hierarchy, quality notes.

### Step 5: Detect structured data (Schema.org)
- Search HTML for JSON‑LD (`<script type="application/ld+json">`) or microdata.
- If found, validate basic syntax (can be done via simple checks). Identify schema types (Organization, Article, Product, etc.).
- If none, flag missing.
- **Output:** schema present? list of types, any obvious errors.

### Step 6: Assess content freshness
- Look for visible dates on the page (publication date, last updated). Use common patterns like `<time>` tags, or text like "Published on ...".
- Also check the `Last-Modified` header from Step 1.
- If no date and header is old (e.g., >1 year), flag as stale.
- **Output:** freshness signal (date found, age estimate).

### Step 7: Identify author/team information
- Look for author bylines (often near title or end of article). Check if author name links to a profile page.
- If author page exists, fetch it and note if it contains bio, credentials, social links.
- **Output:** author presence, profile quality.

### Step 8: Internal linking assessment
- This may require crawling or asking the user. If the user has provided the codebase or you can guess, note any obvious orphan status.
- Otherwise, use `AskUserQuestion` to inquire: "Do you know if this page is linked from other pages on the site? If yes, from which sections?"
- **Output:** internal linking note (Well‑linked / Possibly orphaned / Unknown).

### Step 9: Category/taxonomy depth
- Look for breadcrumbs or category links. If the site has a blog, check if posts are categorised.
- Note if categories are meaningful (e.g., "Strategy", "Growth") vs default "Uncategorized".
- **Output:** taxonomy depth (None / Shallow / Deep).

### Step 10: Summarize findings in a structured report
Create a final report with the following sections:

**1. Executive Summary** – one‑paragraph verdict on AI extractability.

**2. Scorecard Table** (as seen in previous audit)

| Signal | Score | Notes |
|--------|-------|-------|
| Sitemap present | PASS/FAIL | (details) |
| Page titles | GOOD/PARTIAL/FAIL | (details) |
| Meta descriptions | GOOD/PARTIAL/FAIL | (details) |
| Headings (H1-H6) | GOOD/PARTIAL/FAIL | (details) |
| Structured data | PASS/FAIL | (details) |
| Open Graph / Twitter tags | PASS/FAIL/UNVERIFIABLE | (details) |
| Clean semantic HTML | PASS/FAIL | (details) |
| Content freshness | PASS/FAIL | (details) |
| Blog/knowledge content | PASS/FAIL | (details) |
| Author/team information | PASS/FAIL | (details) |
| Internal linking structure | GOOD/POOR | (details) |
| Category/taxonomy depth | GOOD/POOR | (details) |

**3. Core Problems** – bullet list of top issues affecting AI extraction.

**4. Recommendations** – priority‑ordered fixes (P0, P1, P2).

**5. Bottom Line** – concise statement of overall readiness.

## Example

The example output should mirror the rich report we saw earlier, with all the above sections.

