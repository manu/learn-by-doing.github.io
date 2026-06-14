---
title: "8.5 Sessions and Login"
parent: Security
nav_order: 5
---

# Exercise 8.5 — Sessions and Login

## The Story

After Exercise 8.2, librarians can log in. But HTTP is stateless — every request the browser sends is independent. When a librarian sends a second request (to view the book list, for example), the server has no memory of the fact that they logged in on the previous request.

Sessions solve this. When a librarian logs in successfully, the server creates a *session* — a small record stored on the server that says "user X is logged in." The browser receives a *session cookie* — a unique ID that it sends with every subsequent request. The server uses that ID to look up the session and know who is making the request.

## What to Do

### Part A — Feel the statelessness problem

After building the login in Exercise 8.2, test this scenario:
1. Log in as a librarian — the login succeeds and you are taken to the home page
2. In the browser, type the URL for the "Add Book" page directly and press Enter
3. Are you still treated as logged in?

Open your Flask code and look at the "Add Book" route. Does it check whether the user is logged in? If not, anyone who knows the URL can add books without logging in at all.

Write down: why does the login in Exercise 8.2 not actually protect any of the other pages?

### Part B — Understand sessions

HTTP is stateless — each request the browser sends is completely independent. The server has no memory of the previous request.

Sessions are a way to store state between requests. Think through the design:
- When a librarian logs in successfully, the server needs to remember this
- On every subsequent request, the browser needs to tell the server "I am the logged-in librarian"
- The server needs to verify this claim

How would you design this? What does the browser need to send? What does the server need to check? Write your design before reading about how Flask implements sessions.

### Part C — Implement sessions in Flask

Look up Flask's `session` object. It works like a dictionary — you can store values in it after a successful login, and read them back on the next request.

Flask sessions require a secret key — a random string used to sign the session data so it cannot be forged. Look up where to set this in a Flask app and what it does.

Update your login route: after a successful login, store the librarian's identity in the session.

### Part D — Protect the restricted routes

Write a helper function that checks whether a session exists. If yes, the request continues. If no, the browser is redirected to the login page.

Apply this check to every route that should only be accessible to logged-in librarians: adding a book, deleting a book, managing members.

### Part E — Add logout and observe with Developer Tools

Add a logout route that clears the session and redirects to the login page.

Now test the full cycle with Developer Tools open (look in Application → Cookies):
1. Log in — observe what appears in Cookies
2. Navigate to a protected page — does it work?
3. Log out — observe what changes in Cookies
4. Try the protected page again — what happens?
5. Close the browser completely, reopen, and visit the protected page — are you still logged in?

Write down what you observe at each step.

## Topics You Will Learn

- HTTP statelessness — why the server does not remember previous requests
- Sessions and session cookies — how state is maintained across requests
- Flask's `session` object — a dictionary stored on the server, identified by a cookie
- The secret key — why it must be secret and random
- Route protection — requiring authentication before allowing access

## Before You Start — Think About This

1. The session cookie contains an ID, not the actual session data. The session data stays on the server. Why is this design more secure than storing the session data in the cookie itself?
2. If the secret key is exposed (accidentally committed to GitHub, for example), what can an attacker do with it?
3. Sessions expire. If a librarian logs in and then does not use the library for two weeks, should they still be logged in? Who decides the expiry time, and where is that configured?

## When You're Stuck

- `from flask import session` — Flask's session object works like a dictionary.
- `session.clear()` removes everything from the session (use for logout).
- If redirecting from inside a helper function, use `return redirect(url_for("login"))` and check the return value in the route.
- The session cookie is visible in browser Developer Tools under Application → Storage → Cookies. Notice that it contains a cryptographic signature, not readable data.

## Once It Works — Go Further

1. Add a "You are logged in as: [username]" indicator to `base.html` that only appears when a session exists. Hide it when the user is not logged in.
2. Look up HTTPS and why sessions are insecure without it. Without HTTPS, anyone on the same network can intercept the session cookie. Write one paragraph explaining what HTTPS prevents and why it is always required in production.
