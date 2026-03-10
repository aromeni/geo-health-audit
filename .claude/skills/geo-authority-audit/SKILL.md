---
name: geo-authority-audit
description: Assesses a website's authority signals – authorship, citations, external recognition, transparency, and trustworthiness for AI citation readiness.
allowed-tools: [WebFetch, Read, AskUserQuestion]
---

# GEO Authority Audit Skill

## Purpose
Evaluate the trust signals and authority indicators on a website. AI engines (like ChatGPT Search, Perplexity, Google SGE) prefer to cite sources that demonstrate expertise, experience, authoritativeness, and trustworthiness (E‑E‑A‑T). This audit identifies strengths and gaps in those signals.

## Instructions

When the user provides a URL, fetch the page and explore important sub‑pages (About, Team, Contact, Blog) as needed.

### Step 1: Author identification
- Look for author bylines on the main page and any blog posts. Note if author names are present.
- If authors exist, check if they link to profile pages (e.g., `/author/name`).
- Fetch any author profile pages found. Evaluate:
  - Bio (length, detail)
  - Credentials (degrees, certifications, years of experience)
  - Photo
  - Links to social/professional profiles (LinkedIn, Twitter, etc.)
  - Other articles by the same author
- **Output:** List of authors, with a quality rating (Detailed / Minimal / None) for each.

### Step 2: Citations and references
- Scan the page for outbound links to external sources. Are they to authoritative domains (.gov, .edu, established orgs, research papers)?
- Look for phrases like "according to", "source:", "as reported by" that indicate citations.
- Check if claims are backed by evidence (e.g., statistics with a link to the source).
- **Output:** Count of outbound links to authoritative domains, and notes on citation quality.

### Step 3: About page and company transparency
- Look for an `/about` page (or similar). Fetch it if present.
- Assess:
  - Does it explain the company's mission, history, and values?
  - Is there information about leadership/team?
  - Are there details about the company's background, founding date, or location?
- **Output:** About page quality (Comprehensive / Minimal / Missing).

### Step 4: Contact information
- Look for a `/contact` page or contact info in footer.
- Is there a physical address? Phone number? Email? (Legitimacy signals)
- Check if the address appears real (not just a PO box) – use your judgment.
- **Output:** Contact info present (Address / Phone / Email / None).

### Step 5: External recognition and profiles
- Look for links to external profiles: LinkedIn, Crunchbase, Wikipedia, industry awards, press mentions.
- Check footer, About page, author pages for `sameAs` links.
- Also look for mentions like "as featured in" with logos.
- **Output:** List of external profiles and recognitions found.

### Step 6: Content freshness
- Look for dates on articles or pages (publication date, last updated).
- If no dates, check the `Last-Modified` header (from earlier fetch).
- Determine if content is regularly updated (e.g., recent blog posts).
- **Output:** Freshness assessment (Recent / Stale / Unknown).

### Step 7: Transparency and policies
- Look for pages like `/privacy-policy`, `/terms-of-service`, `/editorial-policy`, `/ethics`.
- These indicate a serious, trustworthy operation.
- **Output:** List of policy pages found.

### Step 8: Summarize findings in a structured report

**1. Executive Summary** – one‑paragraph verdict on authority and trustworthiness.

**2. Authority Scorecard** (table)

| Signal | Score | Details |
|--------|-------|---------|
| Authorship | GOOD/PARTIAL/POOR | Named authors, bios, credentials |
| Citations & sources | GOOD/PARTIAL/POOR | Outbound links to authoritative domains |
| About page | GOOD/PARTIAL/POOR | Completeness |
| Contact info | GOOD/PARTIAL/POOR | Address, phone, email |
| External recognition | GOOD/PARTIAL/POOR | LinkedIn, awards, press |
| Freshness | GOOD/PARTIAL/POOR | Recent updates |
| Transparency policies | GOOD/PARTIAL/POOR | Privacy, terms, editorial policy |

**3. Detailed Findings** – paragraphs on each signal.

**4. Core Problems** – bullet list of top authority gaps.

**5. Recommendations** – priority‑ordered fixes (P0, P1, P2) to boost authority and trust.

**6. Bottom Line** – overall authority readiness.

## Example

**User:** "Audit authority for atogstrategy.com"

**Agent:**
- Authorship: One author (Eleonora) but no bio, credentials, or profile page – **POOR**.
- Citations: No outbound links to authoritative sources – **POOR**.
- About page: Missing (404) – **POOR**.
- Contact info: None found – **POOR**.
- External recognition: None – **POOR**.
- Freshness: Content 4+ years old – **POOR**.
- Transparency policies: None – **POOR**.

**Recommendations:** Add author bios, link to sources, create About and Contact pages, establish social profiles, and publish fresh content.
