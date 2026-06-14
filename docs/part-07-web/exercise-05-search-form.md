---
title: "7.5 Search Form"
parent: Web Architecture
nav_order: 5
---

# Exercise 7.5 — Search Form

## The Story

The book list page is live. The librarian opens it, sees 10,000 books, and starts scrolling. After scrolling for thirty seconds without finding what she needs, she stops.

"Can I search? Instead of scrolling through all of them?"

This is exactly the problem search solves. But before building the search box, think about what needs to happen:

1. The librarian types a word into a box on the page
2. The browser sends that word to the server
3. The server queries the database for matching books
4. The server sends back a page with only those books
5. The browser shows the results

Every step in that chain involves something you have not built yet. This exercise builds them all.

## What to Do

### Part A — Build the search form

Create `templates/search.html`. It should have a text input where the librarian types her search, a button to submit, and a results section below.

When no search has been submitted yet, the results section should be empty. When a search has results, it shows a table of matching books. When a search has no results, it says so — "No books found for 'xyz'" — not an empty table.

Think about what the page looks like in each of these three states before you write any HTML.

### Part B — Handle the search in Flask

Add a `/search` route. This route must work correctly in two situations:
- Someone visits `/search` with nothing typed yet
- Someone visits `/search?q=mystery` after typing "mystery"

The route reads the search term, queries the database for books whose titles contain that word, and passes the results to the template.

### Part C — Test the edges

A form that works with clean input is not a complete form. Test each of these and make sure the page handles them without crashing or showing incorrect results:
- The user clicks Search without typing anything
- The user searches for a word with no matches
- The user types only spaces
- The user types a word containing an apostrophe like `O'Brien`

For the apostrophe case: try building the SQL query by joining the search term directly into the SQL string. What happens? This is a preview of Exercise 8.3.

### Part D — Link it from navigation

Add "Search" to the navigation bar in `base.html`. The link should take the librarian directly to the search page.

## Before You Start — Think About This

1. The search form uses GET — the search term appears in the URL as `?q=mystery`. Why is this a good choice for search? What benefit does having the query in the URL provide?
2. The route must handle two cases: a visit with no query, and a visit with a query. How does the route know which case it is? What does it receive from Flask when the query is absent?
3. The template needs to show different content depending on whether the user has searched, and whether the search found anything. These are two separate conditions. Draw the three states on paper before writing any template code.

## When You're Stuck

- HTML forms use the `action` attribute to specify where the form sends its data, and the `method` attribute to specify GET or POST. For search, use GET.
- To read what the user typed, Flask provides a way to access query parameters from the URL. Look up how to read query parameters in the Flask documentation.
- When building SQL queries with user input, use placeholders — a `?` in the SQL string where the value goes, with the actual value passed separately. Never join user input directly into the SQL string. Look up "parameterised queries" to understand why.
- To search for books *containing* a word, not just books *starting with* a word, look up the SQL `LIKE` operator and the `%` wildcard.

## Once It Works — Go Further

1. Add a dropdown to the search form so the librarian can choose to search by title, by author, or by year. The SQL query should change based on which field she selects.
2. Highlight the search term wherever it appears in the results — so "mystery" is visually marked in every matching title. Think about where this logic belongs: in the template, or in a Python helper function.
