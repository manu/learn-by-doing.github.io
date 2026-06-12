---
title: "8.3 SQL Injection"
parent: Security
nav_order: 3
---

# Exercise 8.3 — SQL Injection

## The Story

SQL injection is one of the oldest and most common vulnerabilities in web applications. It appears in the OWASP Top 10 list of critical security risks every year. It has been used to steal millions of user records, delete entire databases, and take down websites.

It works because of one mistake: building a SQL query by concatenating user-provided text directly into the query string.

You are going to break your own application.

## What to Do

### Step 1 — Introduce the vulnerability

In your `/search` route, change the SQL query to use string concatenation instead of parameterised queries:

```
query = "SELECT * FROM books WHERE title LIKE '%" + search_term + "%'"
cursor.execute(query)
```

This is the vulnerable version. Do not use this in a real application.

### Step 2 — Search normally

Search for `history`. It works. The query becomes:
```
SELECT * FROM books WHERE title LIKE '%history%'
```

### Step 3 — Break it

Now search for this exact string:
```
%' OR '1'='1
```

Write down what the full SQL query looks like after substitution. What does it return?

Then try:
```
%'; DROP TABLE books; --
```

Write down what this query looks like. Does it execute? What would happen if it did?

Then try:
```
%' UNION SELECT username, password, id FROM librarians --
```

Write down what this returns. You have just read data from a table that the search function was never supposed to access.

### Step 4 — Document what happened

For each injection attempt:
1. Write the original query template
2. Write the full query after the user input was substituted
3. Describe what the database did
4. Describe what an attacker could do with this

## What You Are Observing

The database cannot distinguish between the query you wrote and the instructions the attacker injected. From the database's perspective, it is all just SQL. The attack works because you trusted user input to be data — but it turned out to be code.

## Topics You Will Learn

- How SQL injection works mechanically
- Why string concatenation in SQL is always dangerous
- The difference between data (values) and code (SQL structure)
- Why user input is never trustworthy

## Before You Start — Think About This

1. The SQL query has two kinds of content: the structure you wrote (the SELECT, WHERE, LIKE) and the data the user provided (the search term). What goes wrong when you mix the two together in a single string?
2. SQL injection is not a Python bug or a Flask bug — it works in any language. What is the common cause across all languages?
3. If you sanitised the input by removing `'` characters before inserting it into the query — would that fix the problem? What other characters might be dangerous?

## Once It Works — Go Further

1. Look up the OWASP Top 10 for the current year. How many of the top 10 vulnerabilities involve trusting user input? What is the common theme?
2. Look up "Bobby Tables" (xkcd.com/327). This famous webcomic explains SQL injection. After Exercise 8.3, you should now understand exactly why it is funny — and why the school lost all its student data.
