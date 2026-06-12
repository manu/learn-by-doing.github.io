---
title: "7.4 Book List Page"
parent: Web Architecture
nav_order: 4
---

# Exercise 7.4 — Book List Page

## The Story

So far your Flask pages return raw HTML strings from Python functions. This works, but it mixes two different concerns in one place: the logic (which books to show) and the presentation (how to display them). As the pages grow more complex, this becomes unmanageable.

Flask has a template engine called *Jinja2* built in. Templates are `.html` files that contain placeholders — `{{ variable }}` — that Flask fills in with real data before sending the page. The Python function handles the logic; the template handles the presentation.

This is the architecture that every Flask application uses.

## What to Do

### Step 1 — Create the templates folder

Inside your project folder, create a folder called `templates/`. Flask looks for templates here automatically.

### Step 2 — Build the book list page

Create `templates/books.html` — a proper HTML page with:
- A navigation bar with links: Home, Books, Search
- A heading: "Library — All Books"
- A table showing all books: title, author, year
- A footer showing the total count: "Showing 247 books"

Use Jinja2 template syntax to inject the book data from Python:
```
{% for book in books %}
    ... one table row per book ...
{% endfor %}
```

Then update the `/books` route in `app.py` to query the database and pass the results to `render_template("books.html", books=book_list)`.

### Step 3 — Add Tailwind CSS

Link Tailwind CSS from a CDN in the `<head>` of your HTML:
```
<script src="https://cdn.tailwindcss.com"></script>
```

Then replace your plain HTML with Tailwind classes to make the page look clean:
- White card for the table on a light grey background
- Alternating row colours
- Clean sans-serif font
- A styled navigation bar

### Step 4 — Create a base template

Create `templates/base.html` with the navigation, head, and footer. Then make `books.html` extend it:
```
{% extends "base.html" %}
{% block content %}
  ... page-specific content here ...
{% endblock %}
```

This means you only need to write the navigation once, and every page inherits it.

## Topics You Will Need

- Flask `render_template()` and the `templates/` folder
- Jinja2 template syntax: `{{ variable }}`, `{% for %}`, `{% if %}`, `{% extends %}`, `{% block %}`
- HTML table: `<table>`, `<thead>`, `<tbody>`, `<tr>`, `<th>`, `<td>`
- Tailwind CSS utility classes for layout, typography, and colour
- Template inheritance: `base.html` with `{% block content %}`

## Before You Start — Think About This

1. What is the advantage of keeping HTML in `.html` files rather than in Python strings? (Think about what happens when a designer wants to change the look, or a programmer wants to change the data.)
2. Jinja2 runs on the server before the page is sent to the browser. The browser receives pure HTML — it never sees the `{{ }}` syntax. Why does this matter for security?
3. Every page in the library will need the same navigation bar. What happens if the navigation bar is duplicated in every template file, and you want to add one more link?

## When You're Stuck

- `render_template("books.html", books=results)` passes `results` to the template as the variable `books`.
- In the template, `{{ book.title }}` assumes each book is a dictionary or an object with a `title` key. SQLite rows from `fetchall()` can be accessed by column name if you set `conn.row_factory = sqlite3.Row` on the connection.
- Start without Tailwind — get the data displaying correctly first, then add styling.
- Tailwind documentation is at `tailwindcss.com/docs` — search for any concept you need (tables, flexbox, colours, spacing).

## Once It Works — Go Further

1. Add pagination to the book list — show 20 books per page, with "Previous" and "Next" buttons. The URL should change to `/books?page=2`, `/books?page=3`, etc.
2. Make the column headers clickable so that clicking "Title" sorts the list by title, and clicking "Year" sorts by year. Look up how to pass sort parameters through the URL.
