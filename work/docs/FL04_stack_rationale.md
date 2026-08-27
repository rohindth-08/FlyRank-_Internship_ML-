# Week 4: Three Roads (Stack Rationale)

## My Constraints
- **Budget:** Free only ($0).
- **Skill Level:** Strong in Python, Pandas, and SQL for machine learning. Capable with basic HTML/CSS, but not an advanced frontend developer (e.g., React/Node).
- **Requirements:** Needs to be a static showcase of my ML-03 and ML-04 case studies. No dynamic backend is required yet.
- **Display Needs:** Must elegantly handle long-form text, Python code blocks with syntax highlighting, and embedded screenshots of Jupyter notebooks and dataframes.

## The Three Options Considered

1. **The Simplest: Plain HTML/CSS on GitHub Pages**
   - *How it works:* Write raw HTML pages and host for free on GitHub.
   - *The Trade-off:* Maintenance is tedious. Adding a new case study means copying and pasting HTML boilerplate and manually formatting Python code blocks line by line.

2. **The Sweet Spot: Markdown Static Site Generator (MkDocs / Astro)**
   - *How it works:* Write case studies in pure Markdown (just like writing in a Jupyter Notebook), and a generator builds the styled site. Hosted on GitHub Pages.
   - *The Trade-off:* Requires a brief 15-minute initial setup to configure the theme, but after that, content creation is frictionless.

3. **The Most Powerful: Next.js / React app**
   - *How it works:* Build custom UI components using JavaScript and deploy via Vercel.
   - *The Trade-off:* Complete overkill. It would require fighting Node/NPM dependencies and React hydration errors just to display static screenshots of dataframes.

## My Decision & Rationale

**I am choosing Option 2 (Markdown Static Site Generator via GitHub Pages).**

I chose this stack because it perfectly aligns with my constraints and my goals as an ML intern. I explicitly rejected the simplest option (raw HTML) because I cannot maintain it efficiently; formatting code blocks by hand would discourage me from updating my portfolio. I also rejected the most powerful option (Next.js) because maintaining JavaScript dependencies is a distraction from my actual focus: machine learning.

A Markdown-based generator like MkDocs or Astro is the clear winner because it answers the two most critical questions:
1. **Can I maintain this?** Yes. Once the config file is set up, adding a new case study is as simple as writing a `.md` text file. The build is entirely automated.
2. **Does it show my work well?** Yes. These tools are built specifically for technical documentation. They handle Python syntax highlighting, long-form reading, and markdown tables perfectly out of the box, ensuring my data contracts and predictive models are the loudest things on the page.
