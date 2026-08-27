# FlyRank ML Internship — Content Decay Prediction

**Predicting which content pages will lose organic search traffic before it happens.**

Built on 79 million rows of real, anonymized FlyRank search data. Deployed as a [live research paper](https://rohindth-08.github.io/FlyRank-_Internship_ML-/paper.html).

---

## What It Does and For Whom

This project builds a **repeatable content decay scoring model** for content strategists managing large portfolios. Instead of waiting for traffic to drop and reacting, the model flags pages *before* significant decay occurs, outputting a ranked action queue with human-readable reason codes (e.g., "HIGH RISK — HIGH TRAFFIC", "STALE — REFRESH CANDIDATE").

**Who it's for:** Content teams, SEO strategists, and anyone managing a portfolio of web content who wants to prioritize refreshes proactively rather than reactively.

---

## Setup (A Stranger Could Follow This)

### Option 1: Google Colab (Zero Install — Recommended)
1. Click the badge below to open the capstone notebook:
   [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/rohindth-08/FlyRank-_Internship_ML-/blob/main/work/notebooks/capstone.ipynb?flush_cache=true)
2. You will need a [HuggingFace token](https://huggingface.co/settings/tokens) with access to the [FlyRank/internship-warehouse](https://huggingface.co/datasets/FlyRank/internship-warehouse) dataset (gated, instant approval).
3. Set your token as a Colab secret named `HF_TOKEN`.
4. Click **Runtime → Run all**. The notebook will pull data via DuckDB over `hf://`, train the model, and export all results.

### Option 2: Local
```bash
git clone https://github.com/rohindth-08/FlyRank-_Internship_ML-.git
cd FlyRank-_Internship_ML-
pip install -r requirements.txt
export HF_TOKEN=your_token_here
jupyter notebook work/notebooks/capstone.ipynb
```

---

## Usage Example

The model outputs a scored CSV queue. Each row is a content page ranked by its probability of decaying >20% in the next 30 days:

| content_hash_id | decay_probability | action | feb_imps |
|---|---|---|---|
| abc123... | 0.82 | HIGH RISK — HIGH TRAFFIC | 12,400 |
| def456... | 0.71 | STALE — REFRESH CANDIDATE | 3,200 |
| ghi789... | 0.55 | MONITOR — EARLY WARNING | 890 |

A content strategist reviews the queue top-down, starting with the highest-risk pages.

---

## Architecture

```
┌─────────────────────┐
│  HuggingFace (hf://) │  ← 79M rows of anonymized search data
└──────────┬──────────┘
           │ DuckDB SQL
           ▼
┌─────────────────────┐
│  Feature Engineering │  ← Feb 2026 aggregates (imps, pos, word count, age)
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│  Label Definition    │  ← Binary: did March imps drop >20% vs Feb?
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│  Random Forest (RF)  │  ← GroupShuffleSplit by client_hash_id
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│  Scored Action Queue │  ← Ranked by decay probability + reason codes
└─────────────────────┘
```

---

## Results (Eval)

| Method | Precision@50 |
|---|---|
| Baseline (>180d stale rule) | Lower |
| RF — Naive Random Split (Leaky) | Higher (inflated) |
| **RF — Grouped by Client (Honest)** | **Real generalization score** |

The gap between the naive and grouped split is itself evidence of how much client-level memorization was happening. Full numbers are generated dynamically in the [capstone notebook](work/notebooks/capstone.ipynb).

---

## Limitations

- **Observational, not causal.** This is cross-sectional data from one portfolio over two months. No controlled experiment was run.
- **Does not predict Google's algorithm.** It models impression changes within this dataset.
- **Static features only.** Word count and category count don't capture real-time content quality.
- **Selection bias.** Only pages with >100 February impressions are included.
- **Single time window.** Feb→Mar 2026. Seasonal effects are not accounted for.

---

## Deliverable Index

| Week | Code | Assignment | Deliverable |
|---|---|---|---|
| 5 | FL-06 | Design Your Personal Agent | [Agent Spec](work/docs/) |
| 5 | FL-07 | Build the Agent | [ArXiv Scout Agent](work/scripts/arxiv_scout_agent.py) + [Build Log](work/docs/FL07_build_log.md) |
| 5 | PF-04 | Personal Website Live | [Live Site](https://rohindth-08.github.io/FlyRank-_Internship_ML-/) + [DNS Walkthrough](work/docs/PF04_dns_walkthrough.md) |
| 6 | ML-09 | Validation Audit | [Notebook](work/notebooks/w06_validation_audit.ipynb) |
| 6 | FL-08 | Make It Do Something | [Explainer](work/docs/FL08_make_it_do_something.md) |
| 6 | FL-09 | Open It on Your Phone | [Fix Log](work/docs/FL09_mobile_fix_log.md) |
| 6 | FL-10 | Survive the Crit | [Critique Doc](work/docs/FL10_survive_the_crit.md) |
| 7 | ML-10 | Content Action Playbook | [Notebook](work/notebooks/w07_action_playbook.ipynb) |
| 7 | FL-11 | Break Your Own Site | [Diligence Doc](work/docs/FL11_break_your_own_site.md) |
| 7 | FL-12 | Plant Your Flag | [Flag Doc](work/docs/FL12_plant_your_flag.md) |
| 8 | ML-11 | Ship the Paper | [Deployed Paper](https://rohindth-08.github.io/FlyRank-_Internship_ML-/paper.html) |
| 8 | ML-12 | Tell the Story | [In Capstone Notebook](work/notebooks/capstone.ipynb) |
| 8 | FL | Impact Project | [Impact Plan](work/docs/FL_impact_project.md) |
| 8 | — | Capstone Story | [Build-in-Public Post](work/docs/capstone_story.md) |
| 8 | — | Build Write-up | [Write-up](work/docs/capstone_writeup.md) |
| 8 | — | Retrospective | [Retrospective](work/docs/retrospective.md) |

---

## AI Transparency

This project was built with an AI coding assistant (Antigravity IDE). Here is exactly what the AI did and what I checked myself:

- **AI did:** Wrote the boilerplate Python code for DuckDB queries, scikit-learn pipelines, HTML/CSS for the portfolio and research paper, and generated initial drafts of documentation.
- **I checked:** Every SQL query against the actual data schema, validated that the grouped split was genuinely honest (by running the intentional leakage test myself), reviewed all claim language to ensure it stayed observational/directional, and made every design decision about feature selection, label thresholds, and the No-Go list.

---

## Data Safety

No client names, domains, URLs, private queries, or raw exports appear anywhere in this repository. All claims use honest language: observed, measured, directional, decision-support.

Built on the [FlyRank ML Internship dataset](https://flyrank.ai).

---

*MIT License. Data use governed by `DATA_USE.md`.*
