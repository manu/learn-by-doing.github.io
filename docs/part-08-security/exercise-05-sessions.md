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

### Step 1 — Enable Flask sessions

Flask sessions require a secret key — a random string used to sign the session cookie so it cannot be forged.

Add to `app.py`:
```
app.secret_key = "a-long-random-string-change-this-in-production"
```

In a real application, this would never be hardcoded — it would be an environment variable. You will see why in Part 10.

### Step 2 — Set the session on login

After a successful login, store the librarian's username in the session:
```
from flask import session
session["username"] = username
```

Redirect to the home page.

### Step 3 — Protect routes

Create a helper function `require_login()` that:
1. Checks whether `"username"` is in the session
2. If yes, returns the username
3. If no, redirects to `/login`

Apply this check to any route that should only be accessible to logged-in librarians (for example: adding a book, deleting a book, managing members).

### Step 4 — Add a logout route

```
GET /logout
```

This route should remove `"username"` from the session and redirect to `/login`.

### Step 5 — Test the session

1. Log in as a librarian — observe the cookie in Developer Tools (Application tab → Cookies)
2. Open a protected route — it should work
3. Log out — observe the cookie changes
4. Try to access the protected route again — you should be redirected to login
5. Close the browser tab, reopen, and navigate to the protected route — are you still logged in?

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
