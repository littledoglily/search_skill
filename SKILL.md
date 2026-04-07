---
name: querit-web-search
description: "Search the web using Querit.ai API. Use when the user wants to search the internet or find current information."
metadata:
  require-secret: true
  require-secret-description: "Enter your Querit.ai API key"
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
- filters: Object. Filter conditions to refine search results. Contains 4 sub-fields:
  - sites: Object. Site filtering.
    - include: Array of strings. Only fetch results from these domains. Empty means no restriction. Example: ["arxiv.org", "github.com"]
    - exclude: Array of strings. Exclude results from these domains. Example: ["reddit.com"]
  - timeRange: Object. Time range filtering.
    - date: String. Supported formats:
      - "d[n]": past n days. Example: "d7" = past 7 days
      - "w[n]": past n weeks. Example: "w2" = past 2 weeks
      - "m[n]": past n months. Example: "m1" = past 1 month
      - "y[n]": past n years. Example: "y1" = past 1 year
      - "YYYY-MM-DDtoYYYY-MM-DD": specific date range. Example: "2024-01-01to2024-06-30"
  - geo: Object. Geolocation filtering.
    - countries: Object.
      - include: Array of strings. Only return results from these countries. Available values: "argentina", "australia", "brazil", "canada", "colombia", "france", "germany", "india", "indonesia", "japan", "mexico", "nigeria", "philippines", "south korea", "spain", "united kingdom", "united states"
  - languages: Object. Language filtering.
    - include: Array of strings. Only return results in these languages. Available values: "english", "japanese", "korean", "german", "french", "spanish", "portuguese"

### Example data inputs

Basic search:
{"query": "latest AI research", "count": 10}

Recent news with time filter:
{"query": "vector database benchmark", "count": 5, "filters": {"timeRange": {"date": "w1"}, "sites": {"include": [], "exclude": []}, "geo": {"countries": {"include": []}}, "languages": {"include": []}}}

Search specific sites in English:
{"query": "RaBitQ quantization", "count": 10, "filters": {"sites": {"include": ["arxiv.org", "github.com"], "exclude": []}, "timeRange": {"date": ""}, "geo": {"countries": {"include": []}}, "languages": {"include": ["english"]}}}

Filter by country:
{"query": "semiconductor news", "count": 10, "filters": {"sites": {"include": [], "exclude": []}, "timeRange": {"date": "d7"}, "geo": {"countries": {"include": ["united states", "japan"]}}, "languages": {"include": []}}}
