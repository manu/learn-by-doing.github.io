---
title: "7.3 First Flask Route"
parent: Web Architecture
nav_order: 3
---

# Exercise 7.3 — First Flask Route

## The Story

In Exercise 7.2, you wrote everything from scratch: parsing the path, building the response headers, converting strings to bytes. It worked — but adding a single new URL required careful manual work.

Flask automates all of that. A *route* in Flask connects a URL path to a Python function. When a request arrives for that path, Flask calls the function and sends back whatever it returns. That is the complete idea.

This exercise rebuilds Exercise 7.2's tiny server in Flask — in about a fifth of the code.

## What to Do

### Step 1 — Install Flask

```
pip install flask
```

Verify it installed:
```
python -c "import flask; print(flask.__version__)"
```

### Step 2 — The simplest Flask app

Create `app.py`. Build a Flask application with three routes:
- `GET /` — returns an HTML page with a heading and a list of book titles
- `GET /books` — returns all books from the database as an HTML list
- `GET /search` — accepts a query parameter `q` and returns matching books

The books should come from `library.db` (your SQLite database from Part 6), not from a hardcoded list.

Expected behaviour:
```
http://localhost:5000/             → Home page with book count
http://localhost:5000/books        → All books as an HTML list
http://localhost:5000/search?q=1984 → Books matching "1984"
```

### Step 3 — Run and verify

```
python app.py
```

Open each URL in the browser. Open the Network tab and compare the request/response to what you built manually in Exercise 7.2. Notice:
- Flask set the status code automatically
- Flask set the `Content-Type` header automatically
- Your function just returned a string — Flask handled everything else

### Step 4 — Connect to the database

Make `/books` and `/search` query `library.db`. Every request should run a fresh query — the function should not store any state between requests.

## Topics You Will Need

- `pip install flask`
- `from flask import Flask, request`
- `@app.route("/path")` decorator
- `request.args.get("q")` — reading query parameters
- `sqlite3` — querying the database inside a route function
- HTML string generation — building an HTML response from Python strings

## Before You Start — Think About This

1. In Exercise 7.2, you wrote a loop that waited for connections. Where is that loop in the Flask version? (It is still there — Flask runs it for you when you call `app.run()`.)
2. A Flask route function receives a request and returns a response. It should not store anything in global variables between requests. Why? (Think: what if two people make requests at the same time?)
3. When you query the database inside a route function, you open a connection, run a query, and close the connection. Should you open one connection for the whole app, or open a new one for each request? What are the trade-offs?

## When You're Stuck

- A minimal Flask route: `@app.route("/"); def home(): return "<h1>Hello</h1>"`
- `request.args` is a dictionary of query parameters. `request.args.get("q", "")` returns the value of `q`, or an empty string if it is missing.
- To run Flask in development mode: `app.run(debug=True)`. This reloads the server automatically when you change the code.
- If you get an error about a database being locked, make sure you are closing the connection after each request: `conn.close()`.

## Once It Works — Go Further

1. Use Flask's `render_template()` instead of building HTML strings in Python. Create a `templates/` folder with an `index.html` file. This is the proper way to build Flask pages — HTML in `.html` files, not Python strings.
2. What happens if the user requests `/books/12345` — a specific book by ID? Add a route that accepts the book ID as part of the URL path (`/books/<int:book_id>`) and returns that book's details.
