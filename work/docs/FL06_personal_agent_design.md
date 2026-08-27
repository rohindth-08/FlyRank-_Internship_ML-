# Agent Spec: The ML ArXiv Research Scout

## 1. Job to be Done
Machine Learning research moves too fast for a single engineer to track. My job as an ML intern requires me to stay updated on new methodologies (especially regarding Search Ranking, Content SEO, and LLMs). 
The job of this agent is to autonomously pull the latest ML research papers from ArXiv every Monday morning, filter out the noise, and output a structured Markdown summary of the top 3 highly relevant papers, explicitly explaining how their methodology could be applied to FlyRank's pipeline.

## 2. The User & Usage Frequency
- **User:** Me (Machine Learning Intern).
- **Frequency:** Weekly. The agent will run autonomously every Monday at 8:00 AM.

## 3. Tools and Data Needed
- **ArXiv API (Data Source):** Free and public access. The agent will query the `/query` endpoint for specific ML categories.
- **LLM Node (Compute):** A Claude 3.5 Sonnet node to read the abstracts, synthesize the methodologies, and filter irrelevant math/physics papers.
- **GitHub / Markdown File Writer (Output Tool):** A tool to push the generated Markdown summary directly into my local repository.

## 4. Draft Instructions (System Prompt)
> "You are the FlyRank ML Scout. Every Monday, you receive a JSON payload of the latest ArXiv papers for 'cs.IR' (Information Retrieval) and 'cs.LG' (Machine Learning). 
> 
> **Your rules:**
> 1. Discard any paper that does not explicitly mention search algorithms, LLMs in ranking, or content decay.
> 2. Select the top 3 most relevant papers.
> 3. For each of the 3 papers, you must output: The Title, The Baseline Model they beat, The New Methodology they propose, and a 2-sentence 'FlyRank Application' explaining how we could use this idea in our pipeline.
> 4. Output strictly in a Markdown table. Do not include pleasantries."

## 5. Five Eval Cases (Pre-Build)
1. **Noise Filtering:** 
   - *Input:* 10 irrelevant quantum physics papers. 
   - *Pass Criteria:* Agent outputs an empty summary or a message saying "No relevant papers found today," rather than hallucinating relevance.
2. **Methodology Extraction:** 
   - *Input:* A dense, highly technical ML paper about ranking. 
   - *Pass Criteria:* Accurately identifies and states the exact baseline model they beat.
3. **Format Strictness:** 
   - *Pass Criteria:* The final output exactly matches the requested Markdown table structure across 5 different test runs.
4. **Missing Data Handling:** 
   - *Input:* A paper returned by the API with a missing abstract. 
   - *Pass Criteria:* The agent flags it with "Abstract Missing - Human Review Required" instead of hallucinating content.
5. **API Failure Recovery:** 
   - *Input:* A 500 Server Error from the ArXiv API. 
   - *Pass Criteria:* The agent catches the error and writes "ArXiv API unavailable" to the markdown file rather than crashing silently.

## 6. Risks & Guardrails
- **Guardrail (What it must confirm):** The agent *must confirm* that the `published_date` of the paper is within the last 7 days. This prevents it from recycling historical papers if the API sorting fails.
- **Guardrail (What it must never do):** The agent *must never* attempt to execute any code or download executable attachments from the papers. It is strictly a read-only summarization pipeline.

## 7. Platform Choice & Justification
- **Chosen Platform:** **n8n** (Self-Hosted/Free version).
- **Justification:** I chose n8n over building a "Custom GPT" (which was the primary alternative considered). A Custom GPT requires me to manually log in, open the chat, and type a prompt every single week. That is just a workflow with extra steps. By using n8n, I can utilize a "Cron Trigger" node so the agent wakes up autonomously every Monday at 8 AM, runs the pipeline, and drops the summary into my folder while I am sleeping. True automation requires autonomy, which n8n provides natively.
