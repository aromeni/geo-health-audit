---
name: geo-mobile-friendly-audit
description: Checks if a webpage is mobile-friendly using Google's Mobile-Friendly Test API. Requires a Google API key with the Mobile-Friendly Testing API enabled.
allowed-tools: [WebFetch, AskUserQuestion]
---

# Mobile-Friendly Audit Skill

## Purpose
Determine whether a webpage is optimized for mobile devices using Google's official Mobile-Friendly Test API.

## Instructions

When the user provides a URL, follow these steps:

1. **Check for API key** – Ask the user: "Do you have a Google Cloud API key with the Mobile-Friendly Testing API enabled? If yes, please provide it. If not, you can enable it in the Google Cloud Console. The API is free with usage limits."
   - If they provide a key, store it for this session.
   - If not, explain that the audit requires an API key.

2. **Call Mobile-Friendly Test API** – Construct the API URL:

https://searchconsole.googleapis.com/v1/urlTestingTools/mobileFriendlyTest:run?key={API_KEY}

Send a POST request with JSON body: `{"url": "URL"}`. Use WebFetch with method POST and appropriate headers (Content-Type: application/json).

3. **Parse the response** – Extract:
- `mobileFriendliness` – either "MOBILE_FRIENDLY" or "NOT_MOBILE_FRIENDLY"
- `mobileFriendlyIssues` – list of issues if not friendly
- `resourceIssues` – any blocked resources
- `screenshot` – optional (not needed)

4. **Summarize findings**:

- **Mobile-Friendly Verdict**: PASS/FAIL
- **Issues found** (if any):
  - [Issue type] – e.g., "Content wider than screen"
- **Recommendations** – based on issues, provide brief guidance.

## Example

**User:** "Check mobile-friendliness for example.com"
**Agent:** (asks for key, returns verdict and issues)
