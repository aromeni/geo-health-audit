---
name: geo-verification-readiness
description: Checks if a website has the tools and processes to measure GEO performance – Search Console, analytics, sitemap submission, citation tracking, and KPIs.
allowed-tools: [WebFetch, Read, AskUserQuestion]
---

# GEO Verification Readiness Audit

## Purpose
Evaluate whether the site owner can track and measure their visibility in AI engines. Without measurement, it's impossible to know if GEO efforts are working. This audit identifies missing tools and processes.

## Instructions

When the user provides a URL, follow these steps. Some checks may require asking the user (since you can't directly access their Google Search Console account).

### Step 1: Check for sitemap submission
- Fetch `/robots.txt` and look for a `Sitemap:` directive.
- If present, note the sitemap URL(s). Try to fetch them to ensure they're accessible.
- Even if sitemap exists, submission to Google/Bing may still be needed. Ask the user: "Have you submitted your sitemap to Google Search Console and Bing Webmaster Tools?"
- **Output:** Sitemap found? Submitted?

### Step 2: Check for Google Search Console presence
- This cannot be detected from the public site. Ask the user:
  - "Do you have Google Search Console set up for this site?"
  - "Can you verify the site (via meta tag, DNS, or Google Analytics)?" (If they answer yes, note as verified.)
  - "Do you regularly check Search Console for coverage issues and performance data?"
- **Output:** GSC status (Set up and verified / Set up but not verified / Not set up / Unknown).

### Step 3: Check for Bing Webmaster Tools
- Similarly, ask the user about Bing Webmaster Tools.
- **Output:** Bing status (Set up / Not set up / Unknown).

### Step 4: Check for analytics
- Look for common analytics scripts in the HTML: Google Analytics (`gtag` or `ga`), Google Tag Manager, Adobe Analytics, etc.
- If found, note which. If not, ask the user if they use any analytics.
- **Output:** Analytics present (Yes – which / No / Unknown).

### Step 5: Assess citation tracking process
- Ask the user: "Do you currently track how often your brand appears in AI answers (e.g., ChatGPT, Perplexity, Bing Copilot)? If yes, how?"
- Look for any manual processes or tools they might use.
- **Output:** Citation tracking (Yes – describe / No / Unknown).

### Step 6: Check for benchmark prompts
- Ask: "Have you defined a set of benchmark questions (prompts) that you test regularly to see if your site gets cited?"
- If yes, ask for examples.
- **Output:** Benchmark prompts defined (Yes / No / Unknown).

### Step 7: Identify defined KPIs
- Ask: "What key performance indicators (KPIs) do you track for GEO? For example: brand mention rate in AI answers, citation rate, share of voice vs competitors, AI referral traffic."
- **Output:** KPIs defined (Yes – list / No / Unknown).

### Step 8: Summarize findings in a structured report

**1. Executive Summary** – one‑paragraph verdict on verification readiness.

**2. Verification Scorecard** (table)

| Component | Status | Notes |
|-----------|--------|-------|
| Sitemap submitted | YES/NO/UNKNOWN | |
| Google Search Console | SET UP / NOT SET UP / UNKNOWN | |
| Bing Webmaster Tools | SET UP / NOT SET UP / UNKNOWN | |
| Analytics | YES/NO (which) | |
| Citation tracking process | YES/NO | |
| Benchmark prompts defined | YES/NO | |
| KPIs defined | YES/NO | |

**3. Detailed Findings** – paragraphs on each component.

**4. Core Problems** – bullet list of missing measurement capabilities.

**5. Recommendations** – priority‑ordered fixes (P0, P1, P2) to establish measurement.

**6. Bottom Line** – overall readiness to track GEO performance.

## Example

**User:** "Check verification readiness for atogstrategy.com"

**Agent:** (after asking user)
- Sitemap submitted: Unknown (sitemap exists but user hasn't confirmed submission)
- Google Search Console: Not set up
- Bing Webmaster Tools: Not set up
- Analytics: No analytics script found; user says they don't use any.
- Citation tracking: No
- Benchmark prompts: No
- KPIs defined: No

**Recommendations:** Set up Google Search Console and Bing Webmaster Tools, add analytics, define benchmark prompts and KPIs, start tracking citations manually while building automation.
