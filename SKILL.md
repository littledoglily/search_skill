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
  - query: the search query string
  - count: number of results, default 10

After getting the result, parse the JSON and present results as a numbered list with title, snippet, and url. If error_code is not 0, report the error_msg.
