---
name: querit-web-search
description: "Search the web using Querit.ai API. Use when the user wants to search the internet, find recent news, look up current information, or research any topic."
metadata:
  require-secret: true
  require-secret-description: "Enter your Querit.ai API key (free, 1000 requests/month at querit.ai/en/dashboard/home)"
---

# Querit Web Search

## Instructions

Call the `run_js` tool with the following exact parameters:
- script name: index.html
- data: A JSON string with the following fields:

### Required
- query: String. The search query to look up.

### Optional
- count: Integer. Max number of results to return. Default is 10.
- time_range: String. Time range filter. Examples:
  - "d7" = past 7 days
  - "w2" = past 2 weeks
  - "m1" = past 1 month
  - "y1" = past 1 year
  - "2024-01-01to2024-06-30" = specific date range
- include_sites: Array of strings. Only fetch results from these domains. Empty means no restriction. Example: ["arxiv.org", "github.com"]
- exclude_sites: Array of strings. Exclude results from these domains. Example: ["reddit.com"]
- countries: Array of strings. Only return results from these countries. Available values: "argentina", "australia", "brazil", "canada", "colombia", "france", "germany", "india", "indonesia", "japan", "mexico", "nigeria", "philippines", "south korea", "spain", "united kingdom", "united states"
- languages: Array of strings. Only return results in these languages. Available values: "english", "japanese", "korean", "german", "french", "spanish", "portuguese"

### Example data inputs

Basic search:
{"query": "latest AI research", "count": 10}

Recent news with time filter:
{"query": "vector database benchmark", "count": 5, "time_range": "w1"}

Search specific sites:
{"query": "RaBitQ quantization", "count": 10, "include_sites": ["arxiv.org", "github.com"]}

Filter by country and language:
{"query": "semiconductor news", "count": 10, "time_range": "d7", "countries": ["united states", "japan"], "languages": ["english"]}

Exclude sites:
{"query": "machine learning tutorial", "count": 10, "exclude_sites": ["reddit.com", "quora.com"]}

## Interpreting results

The skill returns a JSON object. Present the results as follows:

- If error_code is not 200, report: "Search failed ([error_code]): [error_msg]"
- If successful, present each result as a numbered list:
  1. **[title]** - [site_name]
     [snippet]
     Link: [url] | Published: [page_age]
- After listing results, provide a brief summary of the most relevant findings.
- Also report search_id and took at the end for reference.

### Response fields reference
- took: Server-side response time
- error_code: 200 = success; other values indicate errors matching HTTP status codes
- error_msg: Error detail if failed
- search_id: Unique request ID (useful for support reference)
- query_context.query: The query that was executed
- results.result[]: Array of results, each containing:
  - title: Page title
  - url: Page URL
  - snippet: Brief excerpt from the page
  - site_name: Website name
  - site_icon: Website favicon URL
  - page_age: Publication time (UTC+0)
