---
title: "6.4 Search and Join"
parent: SQL as a Solution
nav_order: 4
---

# Exercise 6.4 — Search and Join

## The Story

The librarian has been patient with the CSV system for months. She finally has a proper database. Now she wants answers.

She comes in on Monday morning with a list:

1. "Which students currently have books borrowed and haven't returned them?"
2. "How many books has each student borrowed this term?"
3. "I need to send a reminder to everyone who has had a book for more than 14 days."
4. "Which book has been borrowed the most times since we started?"
5. "Show me all the books that Priya has ever borrowed, with the dates."

With the CSV system, answering any one of these questions would require writing Python that loads two files, loops through both, and manually connects records. It would be 30 lines of code for a single question. And if you changed the CSV format, all that code would break.

You are about to learn to answer all five questions in SQL — a language designed specifically for asking questions about data.

## What to Do

### Part A — Add members and loans

First, populate the database with enough data to ask real questions. Add at least five members and at least fifteen loan records — some already returned, some still out, some overdue. Use a spread of dates so the overdue query has something to find.

Do this by writing `INSERT` statements. Do not add the data by hand in DB Browser — writing the statements yourself is part of learning the language.

### Part B — Answer the librarian's questions

Write a SQL query for each of the five questions above. Run each query in DB Browser's SQL editor first, before adding anything to the Python program.

For each query, write down:
- The question in plain English
- The SQL you wrote
- The result

Work through the simpler queries first (counting books per member) before attempting the ones that require connecting two or three tables.

### Part C — Connect the Python program

Once the queries work in DB Browser, connect three of them to the library menu. When the librarian selects "Current loans" from the menu, the program should run the right query and display the results.

### Part D — Compare to the Python equivalent

Pick the "all books borrowed by Priya" question. Write the equivalent Python code that answers the same question using only lists and loops, without any SQL. Compare the two:
- How many lines of code?
- How does each perform with 10,000 members and 50,000 loans?
- Which is easier to modify if the requirement changes?

## Before You Start — Think About This

1. A JOIN connects two tables using a shared column. When you join `loans` and `books`, what column links them? Write the connection in plain English before you write any SQL.
2. If a member has borrowed 5 books, and you join `members` to `loans`, how many rows come back for that member? Is that a problem, or is that exactly what you want?
3. To count "how many books each member has borrowed", you need to group the results by member and count within each group. Think about this in plain English before touching the keyboard.

## When You're Stuck

- `SELECT` retrieves rows. `WHERE` filters which rows. `ORDER BY` sorts them. `LIMIT` cuts the result to N rows. Look up each if you haven't used them.
- A JOIN links two tables on a matching column. The pattern is: `JOIN other_table ON this_table.column = other_table.column`. You can chain multiple JOINs.
- To count rows grouped by a value, look up `GROUP BY` and `COUNT(*)`. To filter groups (not individual rows), look up `HAVING`.
- For partial text matching, look up `LIKE` in SQL and how to use the `%` wildcard.
- For date comparisons in SQLite, look up `date('now', '-14 days')`.

## Once It Works — Go Further

1. Write a query that finds every member who has *never* borrowed any book — no loans at all. This requires a different kind of join. Look up `LEFT JOIN` and what happens when the right side has no match.
2. The librarian wants a monthly report: the top 5 most borrowed books for the past 30 days. Write the query.
