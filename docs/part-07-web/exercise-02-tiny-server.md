---
title: "7.2 Tiny HTTP Server"
parent: Web Architecture
nav_order: 2
---

# Exercise 7.2 — Tiny HTTP Server

## The Story

Now that you have seen what an HTTP request looks like, you will build the thing that responds to one.

You will not use Flask. You will not use any web framework. You will write a server from scratch using Python's built-in `http.server` module — so that you understand exactly what a web framework is doing for you when you eventually use one.

This server will do one thing: receive any HTTP request and respond with a hand-written HTML page.

## What to Do

### Step 1 — Write the server

Create a file called `tiny_server.py`. Using Python's `http.server` module, write a server that:
- Listens on port 8000
- For any GET request to `/`, responds with an HTML page that shows "Library Home" as a heading and lists three book titles as a bullet list
- For any GET request to `/books`, responds with plain text: "Book list goes here"
- For any other path, responds with a 404 status code and the text "Page not found"

Expected behaviour when you open `http://localhost:8000` in a browser:

```
Library Home
• Sapiens
• 1984
• The Alchemist
```

### Step 2 — Run it and watch it in the Network tab

Start your server:
```
python tiny_server.py
```

Open `http://localhost:8000` in the browser. Watch the Network tab. Observe:
- The request your browser sent
- The response your server sent back (including your HTML)
- The status code

Then open `http://localhost:8000/books` and `http://localhost:8000/anything` and observe the different responses.

### Step 3 — Look at your print statements

Add `print()` calls in your server so that every time a request arrives, it prints the method, path, and any headers. Watch the terminal as you navigate in the browser.

This is exactly what every web framework does internally — it receives the request, reads the path and method, and decides how to respond.

### Step 4 — What Flask does for you

After completing Steps 1–3, write a short paragraph (3–5 sentences) describing what you had to handle manually in your tiny server. What would Flask need to automate to make this easier? This paragraph is your justification for using Flask in Exercise 7.3.

## Topics You Will Need

- `http.server` module — `BaseHTTPRequestHandler`, `HTTPServer`
- `self.path` — the requested URL path
- `self.send_response()`, `self.send_header()`, `self.end_headers()`, `self.wfile.write()`
- HTML basics — `<h1>`, `<ul>`, `<li>`, `<html>`, `<body>`
- `encode()` — converting a Python string to bytes for the HTTP response

## Before You Start — Think About This

1. Your server needs to run continuously, waiting for requests. What kind of loop does this require?
2. HTTP responses have three parts: a status line, headers, and a body. What information goes in each part? (You saw this in Exercise 7.1.)
3. HTML is just text. The browser receives a string from your server and renders it as a visual page. What tells the browser that the string is HTML and not plain text?

## When You're Stuck

- `self.wfile.write(b"<h1>Hello</h1>")` sends the body. The `b` prefix makes it a bytes literal — HTTP responses are bytes, not strings. Or use `"<h1>Hello</h1>".encode()`.
- The `Content-Type` header tells the browser what kind of data it is receiving. For HTML: `text/html`. For plain text: `text/plain`.
- If the browser shows a blank page, check your terminal — there may be a Python error being printed there.

## Once It Works — Go Further

1. Make the server read book titles from `library.csv` and include them in the HTML response dynamically. The page should reflect the actual contents of the file, not hardcoded titles.
2. Write a second endpoint `/search?q=word` that reads the query parameter from the URL and filters books whose titles contain that word. This is the foundation of how search forms work.
