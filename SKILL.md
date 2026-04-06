---
name: querit-web-search
description: "Search the web using Querit.ai API"
metadata:
  require-secret: true
  require-secret-description: "Enter your Querit.ai API key"
---

Search the web using Querit.ai.

Call ai_edge_gallery_get_result with JSON: {"query": "search terms", "count": 10}

Return results as a numbered list with title, snippet, and url.
