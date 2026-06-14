---
title: "7.6 GET vs POST"
parent: Web Architecture
nav_order: 6
---

# Exercise 7.6 — GET vs POST

## The Story

Your search form works. The URL looks like this after a search:

```
/search?q=sapiens
```

That URL is shareable. Paste it in a chat message and anyone who clicks it gets the same search results. That is useful.

Now the librarian asks you to build a form to add a new book. You reuse the same form technique with `method="GET"`. After submitting, the URL looks like this:

```
/add?title=The+Art+of+War&author=Sun+Tzu&year=500+BC&description=A+classic+text+on+strategy...
```

The librarian adds a book with a long title and a description. The URL grows to 800 characters. She tries to copy the URL to show a colleague. The browser truncates it.

Then she realizes something worse: if she presses the Back button and clicks Forward again, the form resubmits — the book gets added *twice*. And if she bookmarks the URL, every time she opens that bookmark, she adds the book again.

GET was the wrong choice.

## The Difference

**GET** sends data in the URL. It is designed for *reading* — fetching, searching, viewing. The URL is the full description of the request. GET requests can be:
- Bookmarked
- Shared
- Cached by the browser
- Stored in history
- Re-run by pressing Refresh

**POST** sends data in the request body, invisible in the URL. It is designed for *writing* — creating, updating, deleting. POST requests:
- Do not appear in the URL
- Are not cached
- Are not re-run by pressing Refresh (the browser warns you first)
- Cannot be bookmarked

The rule: **GET to read, POST to write.**

## What to Do

### Part A — Experience GET for form submission

Build an "Add Book" form at `/add` using `method="GET"`. Submit a book. Observe what happens to the URL. Then:

1. Copy the URL and paste it into a new browser tab. What happens?
2. Press Refresh on the results page. What happens?
3. Try submitting a book with a very long title and description. What does the URL look like?

Write down exactly what you observe for each of these three experiments.

### Part B — Switch to POST and observe the difference

Change the form to `method="POST"`. In Flask, a POST route is defined like this:

```python
@app.route("/add", methods=["POST"])
```

Data from a POST form is read with `request.form.get("title")` instead of `request.args.get("title")`.

Now repeat the three experiments from Part A:
1. Can you copy the URL and paste it into a new tab to re-add the book?
2. What happens when you press Refresh on the results page?
3. What does the URL look like after submission?

Write down what changed.

### Part C — The redirect after POST

When a POST form submits successfully, Flask should not return a page directly. It should *redirect* the user to another page (like the book list). This is called the **Post-Redirect-Get** pattern.

Why? If Flask returns a page directly after POST, pressing Refresh re-sends the POST — the book gets added again. If Flask redirects to a GET request instead, Refresh only re-fetches the list — safe.

Implement this: after a successful book addition, use `redirect(url_for("book_list"))` to send the user to the book list page. Test that Refresh no longer causes a double-add.

### Part D — When to use which

For each of these actions, decide: GET or POST? Write one sentence explaining why.

1. Search for books by title
2. Add a new book to the library
3. Delete a book
4. View the details of a book
5. Update a book's information
6. Export the book list as a CSV file
7. Log in to the system
8. Log out of the system

## Topics You Will Learn

- GET: data in URL, for reading, safe to repeat
- POST: data in request body, for writing, not safe to repeat
- `request.args` (GET) vs `request.form` (POST) in Flask
- The Post-Redirect-Get pattern and why it prevents double-submissions
- HTTP methods as a contract between browser and server

## Before You Start — Think About This

1. A password field uses POST. What would happen if a login form used GET instead? What would the URL look like?
2. When you click a link on a webpage, which HTTP method does the browser use — GET or POST? Why does that make sense?
3. An engineer once said: "GET requests should never change the state of the server." What does "state of the server" mean, and why is this rule important?

## When You're Stuck

- In Flask, `@app.route("/add", methods=["GET", "POST"])` allows both methods on the same route. You can check which method was used with `if request.method == "POST":`.
- `from flask import redirect, url_for` — you need both of these imports to do the Post-Redirect-Get.
- If the browser warns you "Are you sure you want to resubmit this form?" when you press Refresh — that is the browser protecting you from a duplicate POST. That warning is a sign you have not yet implemented the redirect.

## Once It Works — Go Further

1. Open your browser's Developer Tools (F12) and go to the Network tab. Submit your GET form and then your POST form. Compare what you see in the network request for each. Where does the form data appear in each case?
2. There are other HTTP methods beyond GET and POST: PUT, PATCH, DELETE. Look them up. Why do browsers only support GET and POST natively in HTML forms, while APIs use all four?
