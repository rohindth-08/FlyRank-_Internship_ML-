# How DNS Works (A Walkthrough)

*Explaining the internet's phonebook to a non-technical project manager.*

Imagine you want to call a friend named "FlyRank." You don't actually know their phone number (like 192.168.1.1), you just know their name. To call them, you open your phonebook, look up "FlyRank," find the number, and dial it. 

**DNS (Domain Name System)** is literally the internet's phonebook. Computers only know how to communicate using IP addresses (long strings of numbers), but humans prefer reading words like `github.com`. DNS bridges that gap.

Here is exactly what happens in the milliseconds after you type a website address into your browser and hit Enter:

## 1. The Resolver (The Librarian)
Your computer asks its designated DNS Resolver (usually provided by your internet service provider, like Comcast or Google) a simple question: *"Hey, do you know the IP address for rohindth-08.github.io?"* 
The Resolver is like a helpful librarian. If it doesn't know the answer immediately, it goes out onto the internet to find it.

## 2. The Nameserver (The Record Holder)
The Resolver eventually talks to an Authoritative Nameserver. This is the server that actually holds the official records for that specific domain. It is the absolute source of truth. 

## 3. The Records (The Answers)
When the Nameserver gets the request, it checks its database. There are two main types of records you need to know about for hosting websites:

- **A Record (Address Record):** This is a direct translation. It says, *"The domain you are looking for points directly to this exact IP address: 185.199.108.153."* The Resolver takes this number, hands it back to your browser, and your browser connects to the server to load the website.
- **CNAME Record (Canonical Name):** This is an alias. Instead of pointing directly to an IP address, it points to *another name*. For example, if I eventually buy the custom domain `rohindth.com`, I wouldn't use an A Record to point it to GitHub's exact server IP, because GitHub might change their IPs tomorrow and break my site! Instead, I would set a CNAME record saying *"rohindth.com is just an alias for rohindth-08.github.io."* When the Resolver sees a CNAME, it says, "Ah, let me go look up the IP address for that second name instead."

## 4. The Response
Once the Resolver gets the final IP address (whether through a direct A Record or by following a CNAME), it gives it to your browser. Your browser then establishes a secure connection (HTTPS) with that IP address, downloads the HTML files, and displays the website on your screen.
