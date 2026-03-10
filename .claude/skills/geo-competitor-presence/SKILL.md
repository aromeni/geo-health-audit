---
name: geo-competitor-presence
description: Performs a basic GEO presence check on a competitor's website, including schema, sitemap, meta tags, and robots.txt. Useful for benchmarking.
allowed-tools: [WebFetch, Read, AskUserQuestion]
---

# Competitor Presence Audit Skill

## Purpose
Quickly assess a competitor's website for foundational GEO signals: schema presence, sitemap existence, meta tags, and robots.txt. This provides a baseline for comparison with your own site.

## Instructions

When the user provides a competitor URL, follow these steps:

1. **Fetch the homepage** – Use WebFetch to get the HTML. Record status.

2. **Check for schema** – Search HTML for `<script type="application/ld+json">`. List the schema types found (e.g., Organization, WebSite, etc.). Note if any are present.

3. **Check meta tags** – Extract:
   - Title tag content
   - Meta description content
   - Open Graph tags (og:title, og:description, og:image)
   - Twitter Card tags

4. **Check robots.txt** – Attempt to fetch `{root}/robots.txt`. Note if present and any interesting directives (e.g., sitemap reference).

5. **Check sitemap** – Try to fetch `/sitemap.xml` and `/sitemap_index.xml`. Note if present and get a rough count of URLs (if XML, can count `<loc>` elements roughly).

6. **Check for author/byline** – Look for byline patterns (e.g., "by Author Name") or author meta tags.

7. **Summarize findings** in a table. If the user has previously provided a client URL (or if they want to compare), ask: "Would you like to compare this with your own site? If yes, please provide your site URL." Then produce a comparison table.

   **Competitor: example.com**

   | Signal | Found? | Details |
   |--------|--------|---------|
   | Schema | Yes/No | Types: ... |
   | Title | Yes | Content |
   | Meta description | Yes/No | Content |
   | Open Graph | Yes/No | List tags |
   | robots.txt | Yes/No | Sitemap referenced? |
   | Sitemap | Yes/No | Approx URL count |
   | Author byline | Yes/No | Pattern |

8. **Provide brief commentary** – How does this competitor compare to typical best practices? Any obvious gaps?

## Example

**User:** "Check competitor presence for https://competitor.com"
**Agent:** Returns the table and notes.
