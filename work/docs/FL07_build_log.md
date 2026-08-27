# FL-07 Build Log: The ML ArXiv Research Scout

**Date:** August 27, 2026  
**Agent Platform:** Scripted Agent (Python)

## Spec Deviation Log
In the FL-06 design spec, I initially planned to build this agent using the **n8n** self-hosted platform to utilize its native cron triggers. 

*Why I cut it:* During the initial build phase, I realized that spinning up a persistent cloud server for n8n (or configuring Docker locally) would easily blow past the 10-hour build limit for this MVP. To deliver a working agent quickly that I could run locally and debug efficiently, I deviated from the spec and shifted to the **Scripted Agent (Python)** track. 

## Iteration 1: The API Connection
- **Action:** Wrote a basic python script `arxiv_scout_agent.py` using `urllib` to hit the ArXiv API (`export.arxiv.org/api/query`).
- **What Broke:** I didn't specify a category or max results limit. The API returned 1000 random papers across all sciences, crashing my terminal output.
- **Fix:** Added `cat:cs.IR` (Information Retrieval) and `max_results=3` to the API query parameters.

## Iteration 2: Relevance Filtering
- **Action:** Tested the script with the new parameters.
- **What Broke:** The script was successfully pulling 3 papers, but they were often broad Machine Learning papers completely unrelated to search ranking.
- **Fix:** Modified the query string to enforce a keyword match: `all:ranking AND (cat:cs.IR OR cat:cs.LG)`. This instantly fixed the noise problem and ensured high relevance for FlyRank.

## Iteration 3: Output Formatting
- **Action:** Added Python's `os` and file I/O libraries to automatically write the parsed XML data into a structured markdown table.
- **What Broke:** The abstracts (`<summary>`) in the ArXiv XML contained raw newline characters, which completely broke the Markdown table rendering when saved to `research_weekly.md`.
- **Fix:** Added a `.replace('\n', ' ')` string manipulation step and truncated the abstract to 200 characters to ensure the Markdown table rendered beautifully.

## Final Status
MVP is complete and successfully running end-to-end. The agent connects to a live external data source (ArXiv API), parses the XML, applies the search constraints, and outputs a perfectly formatted Markdown file to the `work/outputs/` directory without any human intervention.
