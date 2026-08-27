# Week 5: Explain It Like You Built It

## The Topic: GitHub Actions & Automated Deployments
*During Week 4, I shipped my "Empty but Live" portfolio page. When I enabled GitHub Pages, I initially got a 404 error, and then I saw a yellow circle spinning in the "Actions" tab. I had an AI explain exactly what was happening behind the scenes.*

## My Explanation (How Deploying Works)

If you've never built a website, you might think hitting "Publish" just flips a switch that magically makes your code visible to the internet. But what actually happens is a lot cooler. 

When I hit "Save" to enable GitHub Pages for my portfolio, I triggered an automated sequence called a **Continuous Deployment pipeline (or an Action)**. 

Here is exactly what that yellow spinning circle meant:
1. **The Spin-up:** GitHub instantly rented a tiny, temporary computer in the cloud for me.
2. **The Checkout:** That computer grabbed a copy of the exact `index.html` file I had just pushed to my `main` code branch. 
3. **The Build & Push:** It packaged that file up and securely copied it onto one of GitHub's massive, public-facing web servers. 
4. **The Green Check:** The temporary computer shut itself down, and my code was now officially hosted and reachable by anyone typing in my URL.

It turns out, writing the code is only half the battle. The other half is getting it onto a server that never sleeps. By using GitHub Actions, every time I update a case study or fix a typo, I don't have to manually rent a server or drag-and-drop files. I just commit my code, and that invisible temporary computer wakes up and handles the entire deployment for me in 30 seconds.
