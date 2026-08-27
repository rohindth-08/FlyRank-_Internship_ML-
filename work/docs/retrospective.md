# Retrospective — Written for the Person I Was in Week 1

Eight weeks ago, I walked into this internship knowing how to write Python and knowing what a Random Forest was from a textbook. I did not know how to take a real dataset, ask it a real question, and ship a real answer that a stranger could read and trust. That gap — between knowing ML concepts and doing ML work — is exactly what this track closed.

## What I Set Out to Do

I set out to build a content decay predictor: a model that could flag web pages likely to lose organic search traffic before it happened. The goal was not to build the most complex model possible, but to build the most *honest* one — something a content strategist could actually use to prioritize their work, backed by transparent methodology and validated on a split that mimicked real deployment conditions.

## What Changed

Almost everything changed from my original plan, and that was the most valuable part.

My first instinct was to use every column in the dataset as a feature and chase the highest accuracy number I could find. Week 3's leakage skill completely rewired my thinking. I learned that a near-perfect score is not a celebration — it is a red flag. When I intentionally added the label column as a feature and watched the score jump to 100%, I understood viscerally why validation design matters more than model selection.

My agent plan changed too. I originally designed an elaborate n8n automation workflow for the ArXiv Research Scout. After spending hours fighting deployment complexity, I made the hardest decision of the track: I scrapped it and rebuilt the agent as a simple Python script. It was humbling, but the scripted version actually worked end-to-end, and the n8n version never would have shipped in time. I learned that shipping something simple beats planning something perfect.

The portfolio evolved the most. What started as a blank HTML page became a responsive, mobile-optimized site with a working contact form, SEO meta tags, a graduate badge, and a full deployed research paper. Each week's assignment added one real layer — and the "Survive the Crit" exercise taught me that the hardest feedback to hear ("I can't tell what you do") is always the most useful.

## What I Would Build Next

I would extend the content decay model into a multi-window predictor. Right now it uses a single Feb→Mar window. A production-grade version would train on rolling 30-day windows across six months, capturing seasonal patterns the current model misses entirely. I would also add a simple Streamlit dashboard so a non-technical content strategist could upload their own data and get a ranked queue without touching a notebook.

## The Three Most Transferable Things I Learned

**1. Validation design is more important than model selection.** A Random Forest on an honest grouped split will always beat a neural network on a leaky random split. The split *is* the claim. If your validation doesn't mimic deployment, your metrics are fiction.

**2. Shipping beats perfecting.** The n8n pivot taught me that a working simple thing is infinitely more valuable than a broken complex thing. Every week I had to choose between adding one more feature or committing what I had. Committing always won.

**3. Honest language is a professional skill.** Before this track, I would have written "our model predicts content decay with 85% accuracy." Now I write "the model provides a directional signal for identifying content at risk of decay, measured on a client-grouped holdout split." The second sentence is harder to write, but it is the one that survives scrutiny. Employers, reviewers, and collaborators all trust the person who names their own limitations before someone else does.

---

If I could say one thing to the person I was in Week 1, it would be this: the model is not the product. The *workflow* is the product — the habit of asking "where does my label come from?", "does my split mimic deployment?", and "do my words match my evidence?" Those three questions will outlast any specific model I ever build.
