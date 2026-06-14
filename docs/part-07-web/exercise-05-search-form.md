---
title: "7.5 Search Form"
parent: Web Architecture
nav_order: 5
---

# Exercise 7.5 — Search Form

## The Story

The book list page shows all books. The librarian needs to find one specific book among 10,000. A search form is the interface to that capability.

This exercise teaches you how HTML forms work, how data travels from the browser to the server, and how the server uses that data to query the database and return relevant results. This is the complete cycle: user types → browser sends request → server runs SQL → server returns HTML → browser displays results.

## What to Do

### Step 1 — Create the search form page

Create `templates/search.html`. It should contain:
- A search input field and a "Search" button
- A results section below that appears only when there are results to show

```
[Search library...      ] [ Search ]

Showing 3 results for "mystery"

Title                    Author          Year
-----------------------------------------------
The Mystery of...        Author A        2001
A Mystery in...          Author B        1998
Mystery at...            Author C        2015
```

### Step 2 — Handle the search in Flask

Add a route for `/search` in `app.py`. This route must handle two cases:

1. **No query** (`GET /search` with no `q` parameter): show the empty search form
2. **With query** (`GET /search?q=mystery`): run the SQL query and show results

The SQL query should use `LIKE '%query%'` to find books whose title contains the search term. Return the results to the template.

### Step 3 — Handle edge cases

Test these cases and make sure the page handles each gracefully:
- Empty search (user clicks Search without typing anything)
- Search that matches no books
- Search term that contains a special character like `'` or `"`
- Very long search term

### Step 4 — Link the search from the navigation

Add a "Search" link to `base.html`. When clicked, it should take the user to the search page.

## Topics You Will Need

- HTML form: `<form method="GET" action="/search">`, `<input type="text" name="q">`, `<button type="submit">`
- Why search uses GET (not POST): the query appears in the URL, making results linkable and bookmarkable
- `request.args.get("q")` in Flask
- Jinja2 `{% raw %}{% if results %}{% endraw %}` conditional
- SQL `LIKE` with parameterised queries (not string formatting — you will understand why in Part 8)

## Before You Start — Think About This

1. A search form uses `method="GET"` — the search term appears in the URL as `/search?q=mystery`. A login form uses `method="POST"` — the password does not appear in the URL. Why is this distinction important?
2. If a user searches for `O'Brien` (with an apostrophe), what happens if you build the SQL query by concatenating strings: `"WHERE title LIKE '%" + query + "%'"`)? Try it. (This is a preview of Exercise 8.3.)
3. When there are no results, the page should say "No books found for 'xyz'" — not just show an empty table. How does the template know whether to show this message?

## When You're Stuck

- Always use parameterised queries: `cursor.execute("SELECT * FROM books WHERE LOWER(title) LIKE ?", ("%" + query.lower() + "%",))` — the `?` is a placeholder that SQLite fills in safely.
- `{% raw %}{% if query %}{% endraw %}` in the template checks whether the user has searched for anything. `{% raw %}{% if results %}{% endraw %}` checks whether any results were found. These are two different conditions.
- The `{% raw %}value="{{ query }}"{% endraw %}` attribute on the input field re-populates the search box after submission so the user can see what they searched for.

## Once It Works — Go Further

1. Add a filter to the search form: a dropdown that lets the user search by title, by author, or by year. The SQL query changes depending on which field they choose.
2. Highlight the search term in the results — wherever the search word appears in the title, wrap it in `<mark>` tags so it stands out. Do this in the template using a Jinja2 filter or a Python helper function.
