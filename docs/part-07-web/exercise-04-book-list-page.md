---
title: "7.4 Book List Page"
parent: Web Architecture
nav_order: 4
---

# Exercise 7.4 — Book List Page

## The Story

The librarian opens the library web page for the first time. The book list appears — but it is raw text, no formatting, no navigation, no way to tell where the page ends. Ten thousand book titles in a single unstyled wall of text.

"This doesn't look like a real system," she says. "The school's canteen has a better website than this."

She is right. The page works technically. But a page that is hard to read is a page that nobody uses.

There is also a code problem. Right now, every route function in `app.py` builds HTML by joining Python strings together. When the navigation bar needs an extra link, you change it in every function. When the table layout changes, you update every function separately. The Python code and the HTML presentation are tangled together.

This exercise separates them properly.

## What to Do

### Part A — Create the book list template

Right now your `/books` route builds HTML inside Python. The goal: move all the HTML into a separate file, and have Python only send the data.

Create a `templates/` folder and a `books.html` file inside it. This file should produce a proper HTML page with:
- A navigation bar with links to Home, Books, and Search
- A heading showing what page this is
- A table with columns for title, author, and year — one row per book
- A footer showing the total number of books

The book data comes from Python. Look up Flask's `render_template()` function — it takes a template filename and keyword arguments, and returns a complete HTML response.

### Part B — Make the page look like a real system

The page works but it is unstyled. Tailwind CSS is a way to style HTML using class names directly on the elements — no separate CSS file to write.

Look up how to include Tailwind CSS in an HTML page. Add it to your template and style the page. Aim for:
- A readable table with visible borders or alternating row colours
- A navigation bar that looks like navigation
- Clean typography — a font that is easy to read

Work from the Tailwind documentation. Search for specific things you need.

### Part C — Create a base template

Every page in the library will need the same navigation bar, the same `<head>` section, and the same footer. Right now if you add another page, you copy all that into a new file. When you want to add one navigation link, you change every file.

A better approach: one base template that all pages inherit. Look up Jinja2 template inheritance — specifically the concepts of `extends` and `block`. Create `templates/base.html` with the shared structure, then rewrite `books.html` so it only contains the parts that are unique to the book list.

Test that the page still looks identical after the refactor.

## Before You Start — Think About This

1. Python handles the logic (which books to fetch, how many). HTML handles the presentation (how they look). What happens when both are mixed together in Python string-building code? Who can change the look without touching the logic?
2. Jinja2 runs on the server and produces plain HTML before sending anything to the browser. The browser never sees the template syntax. Why does this matter — what would happen if the browser had to run the template itself?
3. If the navigation bar is duplicated in every template, and you want to add one more link, you must change N files. What is N as the app grows? What is N with template inheritance?

## When You're Stuck

- Flask's `render_template()` passes Python variables to the template. Look up how to access those variables inside the template to display list data row by row.
- SQLite returns rows as tuples by default. To access columns by name (like `book.title`), look up `sqlite3.Row` and how to set it as the `row_factory` on the connection.
- Start with no styling — get the data displaying correctly in a plain HTML table first. Add Tailwind only after the data is right.
- Tailwind's documentation is searchable. Look up specific things: "tailwind table", "tailwind navbar", "tailwind card".

## Once It Works — Go Further

1. The librarian would like to see the list paginated — 20 books per page, with Previous and Next links. The URL should change to `/books?page=2` for the second page. How do you pass the page number through the URL and use it in the SQL query?
2. Can the column headers be clickable links that sort the table? Clicking "Title" should sort by title; clicking "Year" should sort by year. Think about how the sort column and direction travel through the URL.
