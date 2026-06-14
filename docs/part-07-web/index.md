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
- What is the difference between GET and POST?

## Then Flask

Only after observing real requests in browser developer tools, and building a tiny HTTP server by hand, will Flask be introduced.

## Key Topics

- Request and response cycle
- GET (read, data in URL) vs POST (write, data in body)
- Jinja2 templates and template inheritance
- HTML form controls: text, textarea, radio, checkbox, select, select multiple
- Server-side form validation
- Post-Redirect-Get pattern

## Exercises

- [7.1 Watch a Request](exercise-01-request-response.md)
- [7.2 Tiny HTTP Server](exercise-02-tiny-server.md)
- [7.3 First Flask Route](exercise-03-first-flask.md)
- [7.4 Book List Page](exercise-04-book-list-page.md)
- [7.5 Search Form](exercise-05-search-form.md)
- [7.6 GET vs POST](exercise-06-get-vs-post.md)
- [7.7 Form Controls](exercise-07-form-controls.md)