# Capstone Build Write-Up

## The Stack and Why I Chose It
I built this portfolio using **Vanilla HTML/CSS** hosted on **GitHub Pages**. 
*Why?* Because speed and simplicity matter. Using a heavy framework like React for a single-page portfolio introduces unnecessary complexity and dependency bloat. GitHub Pages provides free, instantaneous deployments, automatic HTTPS, and direct integration with my code repository. It is the perfect lightweight stack for this job.

## The Hardest Break
The most difficult challenge was mobile responsiveness (FL-09). Initially, the portfolio looked great on a desktop browser, but when I tested it on a physical phone, the touch targets for my links were much too small to tap accurately, and the container padding squished the text awkwardly. I had to learn how to write precise CSS `@media` queries to stack the layout vertically and expand the button sizes specifically for mobile viewports.

## What I Would Build Next
The next step is to expand the "ML Capstone Work" section of the site. I plan to take the Random Forest Content Decay model I built in week 5 (ML-08), write a detailed technical breakdown of the feature importances, and host an interactive visualization of the model's metrics directly on the portfolio.
