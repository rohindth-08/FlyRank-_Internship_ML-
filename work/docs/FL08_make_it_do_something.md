# Make It Do Something (FL-08)

## The Dynamic Feature: A Working Contact Form
I have added a dynamic contact form to my portfolio so that visitors can message me directly. 

## The Explainer: How Data Flows

**What is a Backend?**
My portfolio is hosted on GitHub Pages. GitHub Pages is just a "Frontend" — it only serves static HTML/CSS files to a visitor's browser. It does not have a database or a server capable of actually executing logic (like sending an email). A **Backend** is the server computer behind the scenes that receives data, processes it, and stores information. 

**How the Data Flows (End-to-End):**
Because I do not have my own backend server, I wired my form to use **Formspree** as a "Backend-as-a-Service". Here is exactly how the data flows:

1. **The User Input:** A visitor types their name and message into the HTML form on my website and clicks "Send Message".
2. **The HTTP POST Request:** My frontend HTML takes that text and sends it as a package of data (an HTTP POST request) securely over the internet directly to Formspree's backend server URL (`https://formspree.io/f/...`).
3. **The Backend Processing:** Formspree's server receives the request, validates that it isn't spam, and executes its backend logic.
4. **The Final Delivery:** Formspree triggers an email and forwards the visitor's exact message directly into my personal email inbox.

This flow takes a completely static HTML poster and turns it into a functional, data-driven tool.
