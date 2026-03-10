---
name: geo-access-audit
description: Checks if a URL is crawlable, indexable, and properly canonicalized for GEO readiness. Use when asked to audit a website's access or crawlability.
allowed-tools: [Bash, WebFetch, Read, AskUserQuestion]
---

# GEO Access Audit Skill

## Purpose
Verify that a given URL can be discovered and processed by search engines and AI crawlers. This is the first layer of a full GEO audit.

## Instructions

When the user provides a URL (or asks to audit a site), follow these steps in order. If any step fails or returns unexpected results, note it clearly in the output.

### Step 1: Fetch the URL and check HTTP status
- Use `WebFetch` to get the URL. Capture the HTTP status code (e.g., 200, 404, 301).
- If the status is a redirect (3xx), follow it and record the final URL. This may indicate a canonicalization issue.
- **Output**: status code, final URL, and any redirect chain.

### Step 2: Check robots.txt
- Extract the domain from the URL (e.g., `https://example.com/page` → `https://example.com`).
- Fetch `robots.txt` using `WebFetch` on `https://example.com/robots.txt`.
- If it exists, parse it to see if the user‑agent `*` (or common bots) disallows the original URL or its path.
- **Note**: Full robots.txt parsing is complex; for this skill, do a simple substring check for the path in `Disallow` lines.
- **Output**: whether robots.txt exists, and whether the URL appears to be blocked.

### Step 3: Check for meta robots and X‑Robots‑Tag
- Using the HTML from Step 1, look for:
  - `<meta name="robots" content="...">`
  - `<link rel="canonical" href="...">`
  - HTTP headers for `X-Robots-Tag` (in the WebFetch response headers).
- Extract the directives (noindex, nofollow, etc.) and the canonical URL if present.
- **Output**: meta robots directives, canonical link, and any X-Robots-Tag.

### Step 4: Check sitemap inclusion
- Try to fetch `sitemap.xml` from the root (e.g., `https://example.com/sitemap.xml`). Also check common locations like `sitemap_index.xml` if needed.
- If a sitemap exists, search for the original URL (or its final canonical URL) inside it. This may require fetching the sitemap and grepping.
- **Output**: whether the URL is listed in a sitemap.

### Step 5: Assess internal discoverability (orphan check)
- This step depends on whether you have access to the site's internal links.
- If the user is auditing their own project and has the codebase locally, you can use `grep` to search for links to the URL.
- Otherwise, ask the user: “Do you know if this page is linked from other pages on the site? If yes, please provide examples.” (Use `AskUserQuestion` tool.)
- **Output**: a note about internal linking (e.g., “Likely orphaned” or “Well linked”).

### Step 6: Summarise findings
Combine all observations into a structured verdict:

- **Access verdict**: Pass / Risk / Fail
- **HTTP status**: …
- **Robots.txt blocking**: Yes/No/Unknown
- **Meta robots directives**: …
- **Canonical tag**: …
- **In sitemap**: Yes/No
- **Orphan risk**: High/Medium/Low
- **Notes**: any additional context

Also provide a short explanation of why the verdict was chosen.

## Example

**User:** "Check access for https://example.com/blog/post"

**Agent:** (after running steps)
- HTTP 200 OK
- robots.txt exists, no disallow for /blog/
- meta robots: index, follow
- canonical: https://example.com/blog/post
- sitemap found, URL is listed
- orphan risk: low (linked from homepage)

**Verdict:** Pass – page is fully crawlable and indexable.

## Important notes
- Always handle cases where robots.txt or sitemap.xml is missing (return “Not found”).
- If a redirect occurs, treat the final URL as the page to audit.
- Use the `WebFetch` tool for all HTTP requests; it returns status, headers, and body.
- If a request fails (timeout, 500), note that as a potential issue.

