---
title: "7.3 First Flask Route"
parent: Web Architecture
nav_order: 3
---

# Exercise 7.3 — First Flask Route

## The Story

You have just built a server from scratch. It works. But to add a new page, you had to: check the path, build the status line, write the headers, add the blank line, convert your string to bytes, write the body. Every single page required every one of those steps, in the right order, every time.

Now imagine adding 20 pages to the library: a book list, a search page, a member list, a loan history, an add-book form. You would copy that entire sequence 20 times. One mistake anywhere — a missing header, a wrong status code — and the browser shows nothing.

Flask is the solution. A *route* in Flask is a Python function connected to a URL path. The function returns content. Flask handles everything else: the status code, the headers, the encoding. Adding a new page means writing one function.

This exercise rebuilds what you built in Exercise 7.2 — in a fraction of the code.

## What to Do

### Part A — Install Flask and understand what it is

Flask is a third-party Python library — it is not built in. Install it using pip (Python's package manager). Verify the installation by checking that you can import it.

Before writing any code, answer this: Flask is often called a "web framework." What does "framework" mean? How is it different from a library? Look it up.

### Part B — Build the same three pages in Flask

Create `app.py`. Build a Flask application with the same three pages you built in Exercise 7.2:
- The root path `/` — library home page with a heading and book list
- `/books` — all books from the database
- A path that does not exist — should return an appropriate error

The books should come from `library.db`, not from a hardcoded list.

Expected behaviour:
```
/             → Home page with book count
/books        → All books as an HTML list
/search?q=1984 → Books matching "1984"
```

### Part C — Compare to the raw server

Run your Flask app and open the same three URLs in the browser. Keep the Network tab open.

Compare what you see to Exercise 7.2:
- Did Flask set the status code correctly without you specifying it?
- Did Flask set the headers without you writing them?
- What did your route function actually have to do?

Write down the differences in lines of code and complexity between the two approaches.

### Part D — Connect search to the database

Add the `/search` route. It should read the query parameter from the URL and search `library.db` for matching books. Every request should run a fresh database query — the function should not cache anything between requests.

## Before You Start — Think About This

1. In Exercise 7.2, you wrote a loop that waited for incoming connections. Where is that loop in the Flask version? It is still running — where did it go?
2. A route function should not store data in global variables. What would go wrong if two students searched at the exact same moment and your function used a global variable to store the results?
3. Should you open one database connection for the entire app, or open a fresh connection for each request? Think through what happens when two requests arrive at the same time.

## When You're Stuck

- Flask uses a `@app.route("/path")` decorator to connect a URL to a function. Look up "Python decorators" if you haven't used them before.
- To read query parameters from the URL (like `?q=history`), Flask provides a `request` object. Look up `request.args` in the Flask documentation.
- Flask's development server has a debug mode that reloads automatically when you change the code. Look up how to enable it.
- If the database appears locked, make sure you are closing the connection at the end of each request.

## Once It Works — Go Further

1. Right now your routes return raw HTML strings built in Python. Flask has a better approach: separate `.html` files with placeholders that Flask fills in. Look up `render_template()` and create a `templates/` folder. This sets up Exercise 7.4.
2. Add a route `/books/<book_id>` that shows the details of one specific book. The book ID comes from the URL itself — Flask can extract it automatically. Look up how.
