# FL-02: Frame It as Cases

## 1. Voice Card
**Voice Card:** "Direct, analytical, plain-spoken, no buzzwords."

*(Note: Add this to your Claude Project Custom Instructions as a standing instruction for future chats).*

---

## 2. Framed Cases

### Case Study 1: Content Opportunity Scoring (FlyRank ML Capstone)

**The Problem**
Editors at large sites waste hours manually guessing which decaying pages to refresh first. A fixed rule (like "update pages older than 6 months") is often too rigid, ignoring actual search demand and the opportunity to recover traffic.

**What I Did**
I built a machine learning ranking model that weighed historical traffic decay against current search volume and average position. I explicitly avoided classifying pages as just "good" or "bad"; instead, I scored them to optimize for Precision@50, ensuring that the top 50 pages recommended were genuinely high-opportunity targets rather than just seasonal noise.

**What Came Of It**
The model successfully generated a prioritized queue of content refresh candidates. It proved that by explicitly capturing subtle decay patterns, a learned ranking can beat a fixed-rule baseline, giving editors a targeted list of where their time is best spent.

---

### Case Study 2: Ranking Signal Analysis

**The Problem**
Marketing teams often chase vanity SEO metrics without knowing which signals actually correlate with sustained organic visibility across large portfolios.

**What I Did**
I ran an Exploratory Data Analysis (EDA) on a 79-million-row warehouse dataset to isolate observable search signals (CTR, impression volume, age) from noise. I grouped the data by client hashes to prevent data leakage and mapped the effect sizes of different metrics to see what actually matters.

**What Came Of It**
I delivered a clean, data-backed signal report identifying the top observable features most heavily associated with traffic retention, giving content teams clear priorities rather than just best guesses.

---

## 3. Bio & CTA Copy

**Bio:** 
I am a data-driven ML engineer who turns raw search data into actionable content strategies. I build models that work on messy real data and I'm honest about their limits.

**Contact / CTA:**
"Let's discuss your content queue. Reach out on LinkedIn or GitHub."

---

## 4. Before/After Example (Generic AI vs. Edited)

**Generic AI (Before):** 
"I leveraged cutting-edge machine learning paradigms to synergize data silos and drive impactful results."

**My Edited Version (After):** 
"I built a ranking model that finds decaying content in messy search data so editors know what to fix first."
