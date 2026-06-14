---
title: "7.2 Tiny HTTP Server"
parent: Web Architecture
nav_order: 2
---

# Exercise 7.2 — Tiny HTTP Server

## The Story

In Exercise 7.1, you watched the conversation between a browser and a server. You saw the request your browser sent and the response the server returned. Now you are going to be the server.

Not with Flask. Not with any framework. You are going to write a server from scratch — because the only way to understand what a framework does for you is to do the work without it first.

Python has a module built into its standard library that lets you do exactly this. No installation required.

## What to Do

### Part A — Write the server

Write a Python script called `tiny_server.py`. Using Python's built-in `http.server` module, build a server that:
- Listens for incoming connections on port 8000
- When a browser visits the root path, responds with an HTML page showing a "Library Home" heading and a list of three book titles
- When a browser visits `/books`, responds with plain text saying the book list goes here
- When a browser visits any other path, responds with a "page not found" message and the appropriate status code

Before writing any code, look up Python's `http.server` module documentation. You need to understand what class to extend and what methods you need to override.

### Part B — Open it in a browser and observe

Run your server. Open a browser and visit `http://localhost:8000`. Keep the Network tab open.

Compare what you see in the Network tab to Exercise 7.1:
- What method is the browser using?
- What status code did your server send?
- What headers did your server include?
- What is in the response body?

Then visit `/books` and a path that does not exist. Observe how the Network tab changes.

### Part C — Add logging to the terminal

Add print statements to your server so that every time a request arrives, the terminal shows: the method, the path requested, and the time.

Watch the terminal as you navigate in the browser. Notice that even loading a simple page can produce multiple requests — the browser may also ask for a favicon, for example.

This logging is exactly what every web framework does internally.

### Part D — Write the case for a framework

After building this by hand, write a short paragraph describing everything you had to handle manually that a web framework would need to automate. What repetitive work did you do? What problems would grow worse as you added more pages?

This paragraph is your justification for using Flask in Exercise 7.3.

## Before You Start — Think About This

1. Your server needs to stay running and wait for connections indefinitely. What kind of structure is required for that? What happens if you close the terminal?
2. HTTP responses have three parts: a status line, headers, and a body. You saw all three in Exercise 7.1. What information goes in each part?
3. The browser receives your response as raw bytes. HTML is text. What does Python require you to do before sending a string as bytes over a network connection?

## When You're Stuck

- The `http.server` module provides a class called `BaseHTTPRequestHandler`. To write a custom server, you extend that class and override methods that handle incoming requests.
- Inside the handler, `self.path` tells you what the browser requested. `self.command` tells you the HTTP method (GET, POST, etc.).
- HTTP responses must be sent in order: first the status code, then the headers, then a blank line, then the body. The module provides methods for each step — read the documentation carefully.
- HTTP response bodies are bytes, not strings. You need to convert your HTML string to bytes before sending it.
- If the browser shows nothing, check your terminal. Python errors print there, not in the browser.

## Once It Works — Go Further

1. Make the `/` page read book titles from `library.csv` and include them in the HTML response. The page should show the actual library contents, not hardcoded titles.
2. Make `/books?q=history` filter books by title and return only matching results. Study the URL — how is the query parameter encoded? How does your server extract it?
