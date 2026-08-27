# ArXiv Scout Agent

An autonomous research assistant that polls the ArXiv API for the latest Machine Learning and AI papers, summarizes them locally, and generates a structured weekly research briefing.

## What It Does & For Whom
**For whom:** Data scientists, ML engineers, and researchers who are overwhelmed by the volume of daily ArXiv submissions.
**What it does:** Instead of scrolling through an unfiltered firehose of PDFs, this agent fetches the top 5 most relevant papers based on custom keywords, extracts the abstracts, and compiles them into an easy-to-read Markdown digest (`research_weekly.md`). 

## Setup (Stranger-Friendly)
To run this agent on your local machine:

1. **Clone the repository:**
   ```bash
   git clone https://github.com/rohindth-08/FlyRank-_Internship_ML-.git
   cd FlyRank-_Internship_ML-/work/scripts
   ```
2. **Install dependencies:**
   This agent only uses standard Python libraries (`urllib`, `xml`, `datetime`). No `pip install` required!
3. **Run the agent:**
   ```bash
   python arxiv_scout_agent.py
   ```
4. **View results:**
   Open the newly generated `research_weekly.md` file in the same directory.

## Usage Example
By default, the agent searches for "Machine Learning" and "Search Ranking". 
```bash
$ python arxiv_scout_agent.py
[Agent] Querying ArXiv API for 'all:Machine Learning AND all:Search'...
[Agent] Successfully retrieved 5 papers.
[Agent] Writing summary to research_weekly.md...
[Agent] Done! Open research_weekly.md to view your briefing.
```
*Output snippet from `research_weekly.md`:*
> **Title:** A New Framework for Content Decay Prediction
> **Authors:** Jane Doe, John Smith
> **Published:** 2026-08-25
> **Abstract:** This paper proposes a novel approach... [Link to PDF]

## Architecture Sketch
```text
┌─────────────────┐       XML      ┌─────────────────┐
│                 │ ─────────────> │                 │
│    ArXiv API    │                │ arxiv_scout.py  │
│                 │ <───────────── │ (Python Script) │
└─────────────────┘  HTTP GET req  └────────┬────────┘
                                            │ Parses XML
                                            │ Formats MD
                                            ▼
                                   ┌─────────────────┐
                                   │                 │
                                   │ research_week.md│
                                   │                 │
                                   └─────────────────┘
```

## V2 Eval Results
In our version 2 evaluation, the agent successfully retrieved and formatted 100% of requested papers (5/5). However, during evaluation, we noticed that ArXiv's API limits result in occasional timeouts if polled too frequently without backoff. The agent was updated to handle XML parsing safely without crashing on empty results.

## Limitations & Guardrails
- **No LLM Summarization (Yet):** Currently, the agent extracts the author-provided abstract rather than using an LLM to generate a custom 1-sentence summary. This keeps the agent fast and free, but requires reading the full abstract.
- **Rate Limiting:** The ArXiv API requires a 3-second delay between requests. The agent currently makes a single batch request, but if extended to page through thousands of results, a rate-limiting sleep function must be implemented to avoid IP bans.
- **Keyword Strictness:** The search relies on ArXiv's native query syntax. If a paper uses "Deep Learning" instead of "Machine Learning", it might be missed unless the query is broadened.

---
*Built with Antigravity IDE (AI Assistant). The AI wrote the XML parsing boilerplate, and I defined the logic, formatting, and limitations.*
