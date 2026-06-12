---
title: Web Architecture
nav_order: 9
has_children: true
---

# Web Architecture

Flask is a framework, not an architecture. Before writing a single line of Flask, you will understand the architecture it sits inside.

## The Architecture

```
Browser
  ↓  (HTTP Request)
Server
  ↓  (SQL Query)
Database
  ↑  (Results)
Server
  ↑  (HTML Response)
Browser
```

## What to Learn First

- What happens when you type a URL and press Enter?
- What is a request? What is a response?
- What is HTML? Why does the browser care about it?

## Then Flask

Only after observing real requests in browser developer tools, and building a tiny HTTP server by hand, will Flask be introduced.

## Exercises

- [Request Response Investigation](exercise-01-request-response.md)