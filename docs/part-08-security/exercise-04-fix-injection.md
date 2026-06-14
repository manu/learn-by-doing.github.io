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

### Part A — Design the fix yourself

Before reading anything about parameterised queries, think through what went wrong in Exercise 8.3.

The database received SQL that contained both your code and the attacker's code, mixed together. The database could not tell the difference — it treated the whole thing as one command.

What would a secure approach look like? Write your theory: how could you send the SQL structure and the user's value to the database in a way that keeps them permanently separate — so the user's value can never become SQL code?

Write this down before you look up the answer.

### Part B — Fix every query in the application

Look up "parameterised queries" in SQLite with Python. Compare what you find to the theory you wrote in Part A.

Now go through your entire application — `app.py` and any other Python files that run SQL — and fix every query that builds SQL using string concatenation or f-strings.

After fixing, run the application. The search should still work for normal queries.

### Part C — Test the same injections again

Run the exact same injection strings from Exercise 8.3 against the fixed search. What happens now?

The injections should produce no results — not because the dangerous characters were filtered out, but because of something more fundamental. Write down why the fix works — what is the database doing differently now?

### Part D — Conduct a full audit

A security audit is a systematic search for a specific class of problem. Do a full audit of your code:
- Find every place where the database is queried
- Verify each one does not join user input into the SQL string
- Mark each one as either "safe" or "needs fixing"

Write down the list. Fix any remaining vulnerable queries.

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
