# Launch, Demo & Story: The Plan to Keep Building

A portfolio that never gets a second project goes stale and stops proving anything new. The difference between a static class artifact and a dynamic career platform is a simple, repeatable habit. 

This document outlines my concrete system to ensure my portfolio remains a living, breathing record of my capabilities as a Machine Learning Engineer.

---

## 1. The Strategy: How to Add the Next Case Study

To avoid the friction of "blank page syndrome" when updating my portfolio, I will not build from scratch. Instead, I am preserving my **Claude Project Context** (which already knows my voice, my tech stack, my formatting rules, and my identity kit). Future updates will be a short conversation with my AI assistant rather than a manual rebuild.

Whenever I complete a new ML project, I will use my preserved AI context to draft a new case study following this exact **3-beat structure**:

### Beat 1: The Problem (The "Why")
*Start with the business pain.*
- **Example:** "Content decays silently over time. Content teams typically wait until SEO traffic has already cratered before reacting, costing clients thousands in lost revenue."

### Beat 2: What I Did (The "How")
*Focus on the technical execution, the data, and the validation.*
- **Example:** "I engineered a data pipeline using DuckDB to process 79M rows of search performance data. I then trained a Random Forest classifier using scikit-learn, strictly evaluating it on a client-grouped holdout split to prevent data leakage and ensure true generalization."

### Beat 3: The Outcome (The "So What")
*End with honest, measured impact.*
- **Example:** "The model successfully identified high-risk pages, achieving a Precision@50 that decisively beat the baseline hard-coded heuristic. This provided content strategists with a ranked, proactive action queue to refresh content *before* traffic drops."

---

## 2. Execution: The Next Real Piece of Work

The first true test of this system will be translating my academic ML Capstone into a portfolio-ready business case study. 

**Target Case Study:** `"The Content Decay Predictor"`

Here is exactly how I will execute the **Launch, Demo, and Story** for this specific project:

### The Launch Plan
- **Where it will go:** A dedicated, highly visual section on the homepage of my portfolio (`index.html`), under the "Recent Work" header.
- **The Asset:** I will link directly to the deployed `paper.html` research paper, which acts as the deep-dive technical artifact backing up my claims.

### The Demo Plan
- **The Video:** I will record a 3-minute screen capture using OBS Studio.
- **The Flow:** I will not use slides. Instead, I will open the live Jupyter Notebook (`capstone.ipynb`), run the cells live, and show the model generating the ranked action queue from raw data.
- **The Honesty Check:** During the demo, I will explicitly mention one limitation on camera (e.g., "The model currently relies on cross-sectional static features like word count, which do not capture real-time content quality"). This proves credibility over hype.

### The Story Plan
- **The Medium:** A "Build-in-Public" post on LinkedIn and the FlyRank showcase thread.
- **The Narrative:** Instead of saying "Look at my accuracy score," the story will focus on *how* I validated the model. I will write about the "leakage epiphany" I had in Week 3, explaining why a grouped client split is infinitely more valuable than a naive random split, framing myself as a rigorous, data-aware engineer.

---

## 3. Accountability: The Concrete Reminder

Intentions do not update portfolios; systems do. I have established a strict cadence to ensure this portfolio scales with my career.

- **The Reminder System:** A recurring Google Calendar event with a mobile push notification.
- **Cadence:** The last Friday of every month at 3:00 PM.
- **Event Title:** 🚀 *Portfolio Maintenance: Add one new win, visualization, or case study.*
- **Checklist within the calendar invite:**
  - [ ] Did I ship anything interesting this month?
  - [ ] Open Claude Project and paste the rough notes.
  - [ ] Ask Claude to format it into the 3-beat structure.
  - [ ] Push the updated HTML to GitHub Pages.
