# The Prompt Ladder

This document tracks the evolution of a prompt from a weak baseline to a highly engineered final version, explicitly examining the output at each step.

---

## 0. The Baseline (Embarrassingly Weak)
**Prompt:** "Write a Python script to find decaying SEO pages."

**Output Excerpt:**
> "Sure! Here is a python script using BeautifulSoup and requests to scrape Google search results for decaying pages..."
> *(Proceeds to write a web scraper that violates terms of service and has nothing to do with my internal analytics data).*

**Notes:**
1. **What changed in the prompt:** N/A (Baseline).
2. **What actually improved in the output:** N/A (Baseline).
3. **What still failed:** The output completely hallucinated the context, assuming "finding pages" meant scraping Google instead of querying a database.
4. **What I would try next:** Give the AI the actual context of the data I have.

---

## 1. Version 1 (+ Real Context)
**Prompt:** "Write a Python script to find decaying SEO pages. I have a CSV called `content_refresh_anonymized.csv` with columns: `content_id`, `impressions_90d`, `clicks_90d`, and `content_age_days`."

**Output Excerpt:**
```python
import pandas as pd
df = pd.read_csv('content_refresh_anonymized.csv')
decaying = df[(df['impressions_90d'] < 100) & (df['clicks_90d'] < 10)]
print(decaying)
```

**Notes:**
1. **What changed in the prompt:** Added real context (file name and schema).
2. **What actually improved in the output:** The AI stopped writing web scrapers and actually wrote pandas code to load my specific file.
3. **What still failed:** The logic for "decaying" is entirely arbitrary (just hardcoding impressions < 100). It also just prints the raw dataframe to the console, which is useless for a 30,000-row file.
4. **What I would try next:** Define a specific output format so it doesn't just dump raw rows.

---

## 2. Version 2 (+ Defined Output Format)
**Prompt:** "Write a Python script to find decaying SEO pages. I have a CSV called `content_refresh_anonymized.csv` with columns: `content_id`, `impressions_90d`, `clicks_90d`, and `content_age_days`. The output should be a new CSV containing only the top 50 pages to review, sorted by highest impressions but lowest clicks."

**Output Excerpt:**
```python
import pandas as pd
df = pd.read_csv('content_refresh_anonymized.csv')
# Sort by highest impressions and lowest clicks
sorted_df = df.sort_values(by=['impressions_90d', 'clicks_90d'], ascending=[False, True])
top_50 = sorted_df.head(50)
top_50.to_csv('top_50_decaying_pages.csv', index=False)
```

**Notes:**
1. **What changed in the prompt:** Added a defined output format (save top 50 to CSV).
2. **What actually improved in the output:** The script is now actionable; it creates a clean file I can hand to an editor instead of printing chaos to the terminal.
3. **What still failed:** The logic is still too simplistic. It grabs brand new pages that just haven't had time to get clicks yet, mistaking "new" for "decaying."
4. **What I would try next:** I need to add constraints to prevent it from using new pages.

---

## 3. Version 3 (+ Constraints) — *The Failure Step*
**Prompt:** "Write a Python script to find decaying SEO pages. I have a CSV called `content_refresh_anonymized.csv` with columns: `content_id`, `impressions_90d`, `clicks_90d`, and `content_age_days`. The output should be a new CSV containing only the top 50 pages to review, sorted by highest impressions but lowest clicks. CONSTRAINT: You must use absolutely no if-statements or pandas filters, only pure math operations."

**Output Excerpt:**
```python
import pandas as pd
import numpy as np
df = pd.read_csv('content_refresh_anonymized.csv')
# Pure math filter using array multiplication
df['is_old'] = np.clip(df['content_age_days'].values - 180, 0, 1) / np.clip(df['content_age_days'].values - 180, 1e-9, 1)
df['score'] = (df['impressions_90d'] * 1000) - df['clicks_90d'] * df['is_old']
df = df.replace([np.inf, -np.inf], np.nan).dropna()
# ... [Unreadable array slicing continues] ...
```

**Notes:**
1. **What changed in the prompt:** Added a strict constraint (no if-statements, only math).
2. **What actually improved in the output:** Nothing. It followed the instruction, but the code became a nightmare.
3. **What still failed:** **This made the output significantly worse.** By forcing the AI into a weird corner, it wrote completely unreadable, buggy Numpy clipping code that crashes on division by zero. The constraint was clever but counter-productive.
4. **What I would try next:** Remove the bad constraint, and replace it with a rule focused on code quality and readability.

---

## 4. Version 4 (+ Quality Criteria)
**Prompt:** "Write a Python script to find decaying SEO pages. I have a CSV called `content_refresh_anonymized.csv` with columns: `content_id`, `impressions_90d`, `clicks_90d`, and `content_age_days`. The output should be a new CSV containing only the top 50 pages to review. Quality Criteria: The code must be highly readable, use standard pandas dataframe filtering (only include pages where content_age_days > 180), and include inline comments explaining the scoring logic."

**Output Excerpt:**
```python
import pandas as pd

df = pd.read_csv('content_refresh_anonymized.csv')

# Step 1: Filter out new pages. We only want pages older than 6 months.
eligible_pages = df[df['content_age_days'] > 180].copy()

# Step 2: Calculate a simple decay score (high exposure, low clicks)
eligible_pages['decay_score'] = eligible_pages['impressions_90d'] / (eligible_pages['clicks_90d'] + 1)
```

**Notes:**
1. **What changed in the prompt:** Removed the bad constraint and added explicit Quality Criteria (readability, standard filtering, inline comments).
2. **What actually improved in the output:** The output is beautiful. It added a `+ 1` to prevent division by zero, explicitly filtered old pages, and explained its math.
3. **What still failed:** The output format is good, but the final CSV headers are messy. I want the final file to look exactly like a specific template so I don't have to rename columns manually.
4. **What I would try next:** Give it an exact example of what a "good" output row looks like.

---

## 5. Version 5 (+ Examples of what good looks like)
**Prompt:** "Write a Python script to find decaying SEO pages. I have a CSV called `content_refresh_anonymized.csv` with columns: `content_id`, `impressions_90d`, `clicks_90d`, and `content_age_days`. The output should be a new CSV containing only the top 50 pages to review. Quality Criteria: The code must be highly readable, use standard pandas dataframe filtering (only include pages where content_age_days > 180), and include inline comments explaining the scoring logic. Example of the final CSV output format:
`Page_ID, Opportunity_Score, Action_Required`
`xyz-123, 95.5, Needs_Refresh`"

**Output Excerpt:**
```python
# ... [filtering and scoring logic] ...

# Step 3: Format the output to match the required template
final_df = top_50[['content_id', 'decay_score']].copy()
final_df['Action_Required'] = 'Needs_Refresh'

# Rename columns to match the exact example
final_df.columns = ['Page_ID', 'Opportunity_Score', 'Action_Required']

final_df.to_csv('top_50_decaying_pages.csv', index=False)
```

**Notes:**
1. **What changed in the prompt:** Added a literal text example of the final output format.
2. **What actually improved in the output:** The script now perfectly formats the final dataframe, renaming the columns and injecting the static "Needs_Refresh" string exactly as shown in the example. 
3. **What still failed:** Nothing. The script runs perfectly and the output requires zero manual cleaning.
4. **What I would try next:** Generalize this prompt into a reusable template for my team.

---

## Final Reusable Prompt

Use this prompt to generate clean, formatted Pandas scripts for scoring datasets:

> **Role:** Act as a Senior ML/Data Engineer.
> **Task:** Write a Python pandas script to process a dataset and output a prioritized ranked queue.
> **Context:** My input file is `[file_name.csv]` containing the following columns: `[list_of_columns]`. 
> **Constraints:** You must filter out rows where `[exclusion_condition, e.g., age < 180]`. 
> **Quality Criteria:** The code must be highly readable, use standard pandas filtering, prevent division-by-zero errors, and include inline comments explaining the math.
> **Output Format:** Save the top `[N]` rows to a CSV. The final CSV must have exactly these columns:
> `[Column_1, Column_2, Column_3]`
> Example row:
> `[Example data 1, Example data 2, Example data 3]`
