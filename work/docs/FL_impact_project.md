# The Impact Project: A System for Continuous Proof

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

The first true test of this system will be translating my academic Capstone into a portfolio-ready business case study.

**Target Case Study:** `"The Content Decay Predictor"`
- **Goal:** Take the deployed research paper and distill it down into a highly visual, 3-beat case study for the "Recent Work" section of my personal website (`index.html`).
- **Focus:** Highlight the difference between a "leaky" naive split and an "honest" grouped split to demonstrate my understanding of rigorous ML validation to hiring managers.

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
