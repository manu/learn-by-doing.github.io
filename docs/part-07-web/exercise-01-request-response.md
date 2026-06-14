---
title: "7.1 Watch a Request"
parent: Web Architecture
nav_order: 1
---

# Exercise 7.1 — Watch a Request

## The Story

You have been building the library system as a command-line program. The librarian uses it by typing commands into a terminal. Now she wants something different: "Can multiple people use this from their own computers? Like a proper website?"

You have used websites your entire life. You know what they look like. But you have never thought about what actually happens between the moment you press Enter in the address bar and the moment the page appears on your screen.

Before building anything for the web, you are going to watch that process happen. This is the most important exercise in Part 7 — everything that follows (routes, responses, forms) is just a structured way of creating the messages you are about to observe.

This exercise has no code. Just observation.

## What to Do

### Part A — Watch a real request

Open any web browser. Look for Developer Tools — in most browsers this is under the menu or opened with a keyboard shortcut (look it up for your browser). Find the **Network** tab. This tab records every conversation between your browser and a server.

With the Network tab open, visit any website. Watch what appears.

Find the first row (the main document request) and click on it. A panel opens. Explore every section in that panel. Write down:
- What did the browser ask for?
- What did the server say in reply?
- What number did the server send to indicate success or failure?
- What type of content did the server send back?

### Part B — Read the actual message

Find the **Response** or **Preview** section of the panel. You are looking at the raw content the server sent — the exact text your browser received and turned into the page you see.

What is it? Copy a small section of it. What does it look like?

### Part C — Investigate three scenarios

Using only the Network tab, investigate and write down your findings for each:

1. Visit a URL on any website that does not exist. What number does the server send back? What does that number mean?
2. Find a search form on any website (a shopping site, a news site) and submit a search. Look at the Network tab. Does the URL change? Where does your search term appear? Is the method different from a regular page visit?
3. Look at any page that has images. How many separate requests did the browser make to fully load the page? Why does loading one page require so many requests?

### Part D — Write your mental model

Based on everything you observed, write a short paragraph (your own words, not copied from anywhere) describing what happens between "pressing Enter in the address bar" and "the page appears on screen." Be as specific as you can. Use the technical terms you encountered.

Keep this paragraph. You will come back to it after Exercise 7.2.

## Before You Start — Think About This

1. When you type a URL and press Enter, your browser sends a request somewhere. How does the browser know *where* to send it? What translates "google.com" into an actual location?
2. The server sends back text. The browser reads that text and shows you a visual page. What tells the browser to treat the text as a page, not as a document to download?
3. The response has a number (200, 404, 500...) and a body (the content). Why are both needed? What does the number tell you that the body cannot?

## When You're Stuck

- Developer Tools is in every browser but has different keyboard shortcuts. Search for "open developer tools" plus your browser name.
- The Network tab may appear empty if you opened it after loading the page. Reload the page with the tab already open.
- Some requests load fast and disappear from view. You can preserve the log — look for a setting like "Preserve log" or "Keep log."

## Once It Works — Go Further

1. Find a request for an image on any page. Look at its Content-Type. How is it different from the Content-Type of the page itself? Why does this make sense?
2. Look at the `User-Agent` header in any request. What information is your browser revealing about itself? Why would a server care what browser you are using?
