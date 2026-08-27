# FL-10 Survive the Crit

## The Proof Statement
*Proof Statement:* "I am a Machine Learning Intern at FlyRank. I turn messy search data into predictive content strategies."

## The Feedback Received (From Peer Reviewer)
**Question 1: In ten seconds, what do I do?**
*Reviewer:* "You do Machine Learning and predict content decay. That part is super clear from the headline."

**Question 2: Would you believe I'm good at it?**
*Reviewer:* "Not yet. You say you build data pipelines, but I don't see any actual proof of work on the page. Also, the 'Download CV' link doesn't do anything, which makes it look broken."

## The Feedback Sort
**Must-Fix:**
1. *Missing Proof:* I need to link to actual work immediately so the reviewer believes my claim. I shouldn't wait for the Capstone to show proof. I will add a "Recent Work" section highlighting the ArXiv ML Agent I built in Week 5 (FL-07).
2. *Broken Link:* The CV link goes nowhere. I must update it to explicitly say "(Coming Soon)" or handle the click gracefully so it doesn't look like a sloppy bug.

**Nice-to-Have (For Later):**
1. *Hover Contrast:* The reviewer mentioned the button hover state could have slightly higher contrast. I will fix this later when I do a full color pass.

## The Fixes Implemented
I did not defend the broken link or tell the reviewer to "just wait for the capstone." Instead, I took the feedback gracefully and immediately updated the live site:
- Added a **"Recent Work"** card directly below the intro, linking to my Python `arxiv_scout_agent.py` code on GitHub as immediate proof of competence.
- Updated the CV link to say "(Coming Soon)" and trigger a Javascript alert so it is an intentional user-state rather than a broken anchor link.
