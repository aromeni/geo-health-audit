---
name: geo-entity-audit
description: Audits a website's entity clarity – how well it defines and distinguishes its organization, products/services, people, and locations for AI understanding.
allowed-tools: [WebFetch, Read, AskUserQuestion]
---

# GEO Entity Audit Skill

## Purpose
Evaluate whether a website makes it easy for AI engines to identify the key real‑world entities (company, offerings, people, locations) and understand their relationships. Clear entities lead to accurate citations and brand representation.

## Instructions

When the user provides a URL, follow these steps. Fetch the main page and explore important sub‑pages (About, Services, Team, Contact) if they exist.

### Step 1: Identify the primary organization
- Look for the company name in the homepage header, footer, or `<title>` tag.
- Is there a dedicated `/about` page? Fetch it and check if it clearly describes the company, its mission, history, and possibly founding date.
- Note if the name is inconsistent (e.g., "Atog Strategy" vs "AtoG").
- **Output:** Company name(s) found, and whether an About page exists with clear description.

### Step 2: Identify products or services
- Scan the homepage and main navigation for mentions of specific services or products.
- Look for a `/services` or `/products` page. Fetch it if present.
- Are offerings named distinctly? (e.g., "Strategy Consulting", "Growth Advisory" – not just "our solutions".)
- Check if each offering has its own dedicated page (or at least a clear section).
- **Output:** List of detected services/products, and whether they have dedicated pages.

### Step 3: Identify people/authors
- Look for author bylines on blog posts (if any). Check if author name links to a profile page.
- Look for a `/team` or `/about#team` section. Fetch it if present.
- For each person found, note if there is a bio, credentials, photo, and links to social/professional profiles.
- **Output:** List of named people, whether they have profile pages, and quality of bio (e.g., "detailed", "minimal", "none").

### Step 4: Identify locations
- Look for address, city, or service area mentions in footer, Contact page, or About page.
- Is there a `/contact` page with physical address, phone, email?
- **Output:** Locations found (if any) – e.g., "London, UK", "Serves Europe".

### Step 5: Assess entity relationships
- Does the About page link to Services? Do author profiles link to the company or to their authored content?
- Is it clear which person offers which service? (e.g., "John leads our Strategy practice.")
- **Output:** Notes on how well entities are connected (Strong / Weak / None).

### Step 6: Check for sameAs / external verification
- Look for links to LinkedIn, Twitter/X, Crunchbase, Wikipedia, or industry‑specific registries in the footer, author pages, or About page.
- These help AI verify entity identity and authority.
- **Output:** List of external profiles found.

### Step 7: Assess naming consistency
- Compare how the company, services, and people are named across different pages. Flag any significant variations (e.g., "AtoG" vs "Atog Strategy").
- **Output:** Consistency note (Consistent / Minor variations / Confusing).

### Step 8: Summarize findings in a structured report

Create a final report with the following sections:

**1. Executive Summary** – one‑paragraph verdict on entity clarity.

**2. Entity Scorecard** (table format)

| Entity Type | Found? | Details | Quality |
|-------------|--------|---------|---------|
| Organization | Yes/No | Name(s), About page | Good/Partial/Poor |
| Services/Products | Yes/No | List, dedicated pages | Good/Partial/Poor |
| People/Authors | Yes/No | Names, profile pages, bios | Good/Partial/Poor |
| Locations | Yes/No | Addresses, service areas | Good/Partial/Poor |
| Relationships | Yes/No | Connections clear? | Strong/Weak/None |
| External Verification | Yes/No | sameAs links count | Good/Partial/Poor |
| Naming Consistency | – | Variations? | Consistent/Minor/Confusing |

**3. Detailed Findings** – for each entity type, a short paragraph describing what was found and any gaps.

**4. Core Problems** – bullet list of top issues affecting entity clarity.

**5. Recommendations** – priority‑ordered fixes (P0, P1, P2) to improve entity definition and AI understanding.

**6. Bottom Line** – concise statement of overall entity readiness.

## Example

The output should mirror the thoroughness of the previous structure audit, with clear tables and actionable recommendations.
