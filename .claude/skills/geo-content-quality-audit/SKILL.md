---
name: geo-content-quality-audit
description: Evaluates webpage content for AI extractability – direct answers, factual density, use of lists/tables, and citable passages.
allowed-tools: [WebFetch, Read]
---

# GEO Content Quality for AI Surfaces Audit

## Purpose
Assess whether the content on a page is written in a way that makes it easy for AI engines (like ChatGPT Search, Perplexity, Google SGE) to extract accurate, citable answers. This goes beyond SEO to focus on readability, structure, and evidence.

## Instructions

When the user provides a URL, fetch the page and extract its main content (ignoring navigation, footers, etc.).

### Step 1: Identify the primary question or intent
- Based on the URL, title, and H1, determine the likely user intent (e.g., "What is X?", "How to Y?", "Best Z for...").
- **Output:** Stated intent.

### Step 2: Locate the direct answer
- Read the first 200 words of the main content.
- Is the question answered directly, or does the page start with marketing fluff ("Welcome to our site..." etc.)?
- A good direct answer is concise, factual, and uses plain language.
- **Output:** Answer location (Immediate / Delayed / Not found) and a snippet of the answer.

### Step 3: Assess use of scannable formats
- Look for:
  - Ordered lists (`<ol>`) – good for steps or rankings.
  - Unordered lists (`<ul>`) – good for features or bullet points.
  - Tables (`<table>`) – excellent for comparisons, specifications, data.
  - Blockquotes, pull quotes – can highlight key points.
- Are these used appropriately for the content?
- **Output:** Count and relevance of lists/tables.

### Step 4: Evaluate factual density
- Scan for specific facts: numbers, dates, percentages, statistics, names, locations.
- Compare to vague language ("high quality", "best in class", "innovative").
- A high‑factual page is more likely to be cited.
- **Output:** Factual density (High / Medium / Low) with examples.

### Step 5: Identify citable passages
- Look for short, standalone sentences that could be quoted directly.
- They should be clear, informative, and not require context.
- For example: "The average response time is 2.4 seconds." vs "We're really fast."
- **Output:** Number of citable passages and examples.

### Step 6: Check for jargon and clarity
- Is the language plain and understandable to a general audience?
- Flag excessive use of industry buzzwords or unexplained acronyms.
- **Output:** Clarity rating (Clear / Moderate / Confusing).

### Step 7: Assess promotional vs. informative balance
- Estimate the proportion of content that is purely promotional ("We are the best...") vs. informative ("Here are the steps...").
- AI prefers informative content.
- **Output:** Balance (Mostly informative / Mixed / Mostly promotional).

### Step 8: Evaluate uniqueness
- Does the content offer original insights, examples, or data, or does it read like generic copy found on many sites?
- If possible, note any signs of originality (case studies, proprietary research, unique examples).
- **Output:** Uniqueness (Original / Somewhat unique / Generic).

### Step 9: Summarize findings in a structured report

**1. Executive Summary** – one‑paragraph verdict on content quality for AI.

**2. Content Quality Scorecard** (table)

| Signal | Score | Details |
|--------|-------|---------|
| Direct answer | GOOD/PARTIAL/POOR | Location and clarity |
| Scannable formats | GOOD/PARTIAL/POOR | Lists/tables used well |
| Factual density | HIGH/MEDIUM/LOW | Examples |
| Citable passages | GOOD/PARTIAL/POOR | Count and quality |
| Clarity | CLEAR/MODERATE/CONFUSING | Jargon level |
| Promotional vs informative | INFORMATIVE/MIXED/PROMOTIONAL | Balance |
| Uniqueness | ORIGINAL/SOMEWHAT/GENERIC | Originality |

**3. Detailed Findings** – paragraphs on each signal with specific examples from the page.

**4. Core Problems** – bullet list of top content quality issues.

**5. Recommendations** – priority‑ordered fixes (P0, P1, P2) to improve extractability.

**6. Bottom Line** – overall content readiness for AI.

## Example

**User:** "Audit content quality for atogstrategy.com"

**Agent:** (based on previous audits, likely all scores low)
- Direct answer: Not found – homepage is generic tagline.
- Scannable formats: None.
- Factual density: Low – no numbers or data.
- Citable passages: None.
- Clarity: Moderate – but content is minimal.
- Promotional vs informative: Mostly promotional (just a tagline).
- Uniqueness: Generic.

**Recommendations:** Write substantive content that directly answers user questions, include data, use lists and tables, and avoid fluff.
