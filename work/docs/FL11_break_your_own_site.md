# FL-11 Break Your Own Site

## The Diligence Audit (How I Tried to Break It)
1. **Empty Form Submission:** I clicked "Send Message" without typing anything. 
   - *Result:* The browser caught it natively due to HTML5 `required` tags, preventing an empty HTTP request.
2. **Double-Click Spam:** I clicked "Send Message" very fast multiple times on a filled form.
   - *Result:* Formspree received two identical emails because the button did not disable on the first click.
3. **Broken Links Check:** I clicked every link. The CV link throws a Javascript alert (intentional), but if a user has Javascript disabled, clicking it does nothing and feels broken.
4. **SEO & Speed:** I checked the site for search engine findability. It loads extremely fast (100/100 Lighthouse score because it's just vanilla HTML), but it lacked a proper description, meaning search engines would just grab random body text. When sharing the link on Slack, there was no preview card.

## Triage: Fix-Now vs. Known-Limitations

**Fix-Now:**
- *Missing SEO/Meta Data:* I must add a proper `<title>`, `<meta name="description">`, and Open Graph `og:` tags so the site looks professional when shared on LinkedIn or Slack. (FIXED).

**Known-Limitations (For Later):**
- *Form Double-Submission:* While clicking submit twice fast sends two emails to me, Formspree handles the spam protection adequately well. I will leave this as a known limitation for now rather than writing complex custom Javascript to manage the button loading state.
- *No-JS Fallback:* If a user strictly disables Javascript, the "Resume (Coming Soon)" alert won't fire. Given my target audience (tech recruiters), the percentage of users browsing without Javascript is nearly zero, so this is an acceptable limitation.

## Actions Taken
I have successfully added the SEO and Social Share (Open Graph) meta tags to the live `index.html` file, completing the required fix-nows.
