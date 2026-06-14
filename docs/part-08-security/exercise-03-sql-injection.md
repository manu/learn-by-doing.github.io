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

### Part A — Introduce the vulnerability

In Exercise 7.5, you built the search form. Look at your `/search` route and find where it builds the SQL query. Is the search term joined directly into the SQL string, or passed separately?

If you already used parameterised queries (with `?` placeholders), temporarily change the search query to use string concatenation instead — join the search term directly into the SQL string. This is the vulnerable version.

Search for a normal word like `history`. It works.

### Part B — Break your own system

Now search for this string exactly as written:

```
%' OR '1'='1
```

Write down what the full SQL query looks like after your search term is substituted in. What did the database return? Why?

Then try:

```
%'; DROP TABLE books; --
```

Write down what this query looks like. Does it execute? If it did execute fully, what would happen to the library?

Then try:

```
%' UNION SELECT username, password, id FROM librarians --
```

Write down what this returns. Which table does this data come from? Was the search supposed to be able to access that table?

### Part C — Document what happened

For each injection attempt, write down:
1. The original query template (with the placeholder where the search term goes)
2. The full query after the search term was substituted in
3. What the database did
4. What an attacker could do with this in a real system

### Part D — Understand why it works

The database cannot distinguish between the SQL you wrote and the SQL the attacker injected. From its perspective, it is all just SQL.

Write one paragraph explaining what the fundamental mistake was. Not "I used string concatenation" — but why string concatenation creates this specific problem. What was trusted that should not have been trusted?

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
