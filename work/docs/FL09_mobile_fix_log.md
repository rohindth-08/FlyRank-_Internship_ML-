# FL-09 Mobile Fix Log

## Mobile Audit (Before)
When opening the portfolio on a physical mobile device, several UX/UI issues were immediately apparent:
1. **Touch Targets Too Small:** The text links (LinkedIn, GitHub, CV) were placed too close together horizontally. They were hard to tap accurately with a thumb without hitting the wrong link.
2. **Padding Overflow:** The side padding on the main container was too wide (`2rem`) for a narrow screen, which squished the text awkwardly into the center.
3. **Typography Sizing:** The main `<h1>` title was slightly too large on narrow displays, causing jarring and uneven line breaks.

## The Fixes (After)
I implemented a mobile-first CSS `@media (max-width: 600px)` query to resolve these accessibility issues:
1. **Fixed Touch Targets:** I converted the inline text links into block-level, pill-shaped buttons with generous padding (`0.8rem`) and a light gray background. I stacked them vertically using `flex-direction: column`. This ensures they are perfectly ergonomic for thumb-tapping on a phone.
2. **Fixed Padding:** I reduced the global body padding to `1.5rem` on mobile, giving the content more room to breathe across the full width of the screen.
3. **Fixed Typography:** I scaled the main heading from `2.5rem` down to `2rem` on mobile screens to ensure it stays on one or two clean lines without dominating the viewport.

*Result:* The portfolio is now fully responsive, readable, and highly usable on a physical phone.
