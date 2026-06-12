---
title: "8.4 Fix the Injection"
parent: Security
nav_order: 4
---

# Exercise 8.4 — Fix the Injection

## The Story

You have seen how SQL injection works. Now you will fix it — and understand why the fix works at a fundamental level, not just "use this instead."

The fix is called *parameterised queries* (also called *prepared statements*). Instead of building one SQL string that contains both the structure and the data, you give the database the structure and the data separately. The database keeps them separate — the data can never become code.

## What to Do

### Step 1 — Fix every query in the application

Go through every place in `app.py` (and any other Python files that run SQL) where a string variable is inserted into a query.

Replace every instance of string concatenation or f-string formatting in SQL with a `?` placeholder:

**Vulnerable:**
```
"SELECT * FROM books WHERE title LIKE '%" + term + "%'"
```

**Fixed:**
```
"SELECT * FROM books WHERE title LIKE ?"
("%" + term + "%",)
```

The second argument to `cursor.execute()` is a tuple of values. SQLite substitutes each `?` with the corresponding value — but it treats those values as data, never as SQL code.

### Step 2 — Test the same injections

Run the same injection strings from Exercise 8.3:
```
%' OR '1'='1
%'; DROP TABLE books; --
%' UNION SELECT username, password, id FROM librarians --
```

What happens now? The injections should produce zero results — not because they were filtered out, but because the database treats the entire string as a literal value to match against, not as SQL to execute.

### Step 3 — Understand why it works

Write a short explanation (3–4 sentences) of why parameterised queries prevent injection. Your explanation should answer:
- What does the `?` placeholder do?
- What is the difference between how the database processes a concatenated query versus a parameterised one?
- Is there any input that could still break a parameterised query?

### Step 4 — Check all database interactions

Do a full audit of your code. Find every `cursor.execute()` call and verify it uses `?` placeholders. This is a security audit — be thorough.

## Topics You Will Learn

- Parameterised queries — the correct way to include user data in SQL
- Why separation of code and data is a security principle, not just a style preference
- How to perform a basic security audit of database code
- The principle of least trust: never trust input from the user

## Before You Start — Think About This

1. Parameterised queries are safer — but are they also faster? Why might the database be able to execute parameterised queries more efficiently than concatenated ones?
2. Some developers "sanitise" input — remove or escape dangerous characters before inserting into the query. Why is sanitisation an unreliable fix compared to parameterisation?
3. If a `?` placeholder prevents the user's input from being interpreted as SQL, what exactly is the database doing differently with parameterised input?

## Once It Works — Go Further

1. Look up *stored procedures* — another technique for separating SQL structure from data. How are they different from parameterised queries? When might you use one over the other?
2. Write a function `safe_search(query)` that wraps your database search, enforces parameterised queries, and raises an exception if anyone tries to pass a pre-built SQL string to it. This is called a *security boundary* — a layer that enforces correct behaviour.
