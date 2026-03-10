---
name: geo-schema-audit
description: Audits a website's structured data (Schema.org) for correctness, completeness, and alignment with page content.
allowed-tools: [WebFetch, Read]
---

# GEO Schema Audit Skill

## Purpose
Evaluate the structured data on a website to ensure it accurately describes the organization, content, and entities to AI engines and search crawlers. Good schema improves citation accuracy and enables rich results.

## Instructions

When the user provides a URL, follow these steps. Fetch the page HTML and extract all structured data.

### Step 1: Extract all schema markup
- Search the HTML for:
  - `<script type="application/ld+json">` blocks (JSON‑LD)
  - Microdata attributes (`itemscope`, `itemprop`, `itemtype`)
  - RDFa (less common)
- For JSON‑LD, try to parse each block. Note any that fail basic JSON parsing.
- **Output:** List of schema blocks found, with their types and a note on parseability.

### Step 2: Identify schema types present
- For each valid block, record the `@type` (or multiple types).
- Common types to look for: Organization, WebSite, Article, BlogPosting, Person, Service, Product, FAQPage, BreadcrumbList, LocalBusiness, Review, AggregateRating.
- **Output:** List of all schema types found across the page.

### Step 3: Check required properties for key types
- For Organization: name, url, logo? (logo recommended)
- For Article: headline, author, datePublished, publisher? (publisher often Organization)
- For Person: name, sameAs? (optional but good)
- For Service: name, description, provider? (provider should be Organization)
- For Product: name, description, offers? (price, availability)
- For FAQPage: mainEntity (Question/Answer pairs)
- **Output:** For each type, note missing required/recommended properties.

### Step 4: Validate alignment with visible page content
- Compare schema claims with what's visible on the page:
  - Does the Organization name match the company name seen in the header/footer?
  - Does the Article headline match the page's H1?
  - Is the author named in schema actually mentioned on the page (e.g., byline)?
  - Are the services/products in schema actually described in the content?
- Flag any mismatches or hallucinations (e.g., schema claims a review that doesn't exist on page).
- **Output:** List of alignment issues.

### Step 5: Check for duplicate or conflicting schema
- Are there multiple Organization blocks with different names?
- Is there both an Article and a BlogPosting on the same page (sometimes fine if one is main entity and other is part of WebPage, but can be confusing)?
- **Output:** Notes on duplicates or conflicts.

### Step 6: Assess coverage across important pages
- If the user provided a single URL, focus on that page.
- Optionally, you can suggest checking other key pages (homepage, about, services, blog posts) and offer to audit them.
- **Output:** Coverage assessment (e.g., "Homepage has Organization, but no Article schema on blog posts.")

### Step 7: Summarize findings in a structured report

**1. Executive Summary** – one‑paragraph verdict on schema health.

**2. Schema Scorecard** (table)

| Aspect | Score | Details |
|--------|-------|---------|
| Schema presence | PASS/FAIL | List of types found |
| Required properties | GOOD/PARTIAL/POOR | Missing key fields |
| Content alignment | GOOD/PARTIAL/POOR | Mismatches with visible text |
| Syntax validity | PASS/FAIL | JSON parse errors? |
| Duplicates/conflicts | PASS/FAIL | Any conflicting blocks |
| Coverage breadth | GOOD/POOR | Key pages covered? |

**3. Detailed Findings** – for each schema block, describe what it claims and any issues.

**4. Core Problems** – bullet list of top schema issues.

**5. Recommendations** – priority‑ordered fixes (P0, P1, P2) with specific code examples.

**6. Bottom Line** – overall readiness.

## Example Output Snippet

**Schema presence:** FAIL – no structured data found on any page.  
**Recommendation:** Add Organization and WebSite schema to homepage, and Article schema to blog posts. Example:

```json
{
  "@context": "https://schema.org",
  "@type": "Organization",
  "name": "Atog Strategy",
  "url": "https://atogstrategy.com",
  "logo": "https://atogstrategy.com/logo.png"
}
