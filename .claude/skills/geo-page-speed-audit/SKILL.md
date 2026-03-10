---
name: geo-page-speed-audit
description: Measures page speed metrics using Google PageSpeed Insights API. Requires a Google API key with PageSpeed Insights enabled.
allowed-tools: [WebFetch, AskUserQuestion]
---

# Page Speed Audit Skill

## Purpose
Evaluate the loading performance of a webpage using Google's PageSpeed Insights API. Provides Core Web Vitals and optimization suggestions.

## Instructions

When the user provides a URL, follow these steps:

1. **Check for API key** – Ask the user: "Do you have a Google Cloud API key with the PageSpeed Insights API enabled? If yes, please provide it. If not, you can get one for free at https://developers.google.com/speed/docs/insights/v5/get-started."
   - If they provide a key, store it for this session.
   - If not, explain that the audit requires an API key and cannot proceed.

2. **Call PageSpeed API** – Construct the API URL:
import os
import dotenv
dotenv.load_dotenv()
API_KEY = os.getenv("GOOGLE_API_KEY")
https://www.googleapis.com/pagespeedonline/v5/runPagespeed?url={URL}&key={API_KEY}

Use WebFetch to GET this URL.

3. **Parse the response** – Extract key metrics:
- Overall performance score (0-100)
- Largest Contentful Paint (LCP)
- First Input Delay (FID) or Total Blocking Time (TBT)
- Cumulative Layout Shift (CLS)
- Time to First Byte (TTFB)
- Whether Core Web Vitals assessment passes (LCP < 2.5s, FID < 100ms, CLS < 0.1)

4. **Extract recommendations** – From the `lighthouseResult.audits` section, collect the top 5 opportunities with the highest impact.

5. **Summarize findings** in a structured format:

- **Overall Performance Score**: X/100
- **Core Web Vitals**:
  - LCP: X.X s (Pass/Fail)
  - FID/TBT: X ms (Pass/Fail)
  - CLS: X.X (Pass/Fail)
- **Other metrics**: TTFB, etc.
- **Top Opportunities**:
  1. [Opportunity title] – Estimated savings
  2. ...

Also include a link to the full report on Google PageSpeed Insights.

6. **Note any errors** – If the API returns an error (e.g., invalid key, quota exceeded), report it clearly.

## Example

**User:** "Run page speed audit on example.com"
**Agent:** (asks for API key, then returns report)
