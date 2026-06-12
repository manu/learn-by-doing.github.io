---
title: "6.4 Search and Join"
parent: SQL as a Solution
nav_order: 4
---

# Exercise 6.4 — Search and Join

## The Story

The library database now has 10,000 books. You can also add members and record loans. But the real power of SQL is not storing data — it is *querying* it. SQL lets you ask questions that would require complex, error-prone Python code using CSV.

This exercise teaches you to read data from the database using `SELECT`, and to connect data from multiple tables using `JOIN`.

## What to Do

### Step 1 — Basic SELECT queries

Open DB Browser's SQL editor (or write a Python script that prints query results). Write and run each of these queries:

1. Show all books published after 2000
2. Show all books where the title contains the word "history" (case-insensitive)
3. Show the 10 most recently published books
4. Count how many books are in the database
5. Count how many distinct authors are in the database

For each query, write it in SQL, run it, and note the result.

### Step 2 — Add test data

Add five members to the `members` table. Then add ten loan records to `loans` — some books borrowed, some returned (set a `returned_date`), some still out.

Do this with `INSERT` statements.

### Step 3 — JOIN queries

A JOIN connects two tables using a shared column. Write queries for:

1. Show the name of every member alongside the title of every book they have borrowed
2. Show all books that are currently on loan (no return date recorded yet)
3. Show all books that a specific member (by name) has ever borrowed
4. Show how many books each member has borrowed (use `GROUP BY` and `COUNT`)
5. Show members who currently have overdue books (borrowed more than 14 days ago, not returned)

### Step 4 — Compare to the Python equivalent

For query 3 (all books borrowed by a specific member), write the equivalent Python code that would do the same thing using two lists and a manual scan. Compare the two approaches in terms of code length, readability, and performance.

## Topics You Will Learn

- `SELECT`, `WHERE`, `ORDER BY`, `LIMIT`
- `COUNT`, `DISTINCT`, `GROUP BY`
- `LIKE` for partial text matching
- `INNER JOIN` — combine rows from two tables where a condition matches
- `LEFT JOIN` — include all rows from the left table even if there is no match
- Aggregate functions: `COUNT`, `SUM`, `AVG`, `MAX`, `MIN`

## Before You Start — Think About This

1. In a JOIN, you are combining rows from two tables. What is the "joining condition"? In the case of loans and books, what column connects them?
2. What is the difference between `WHERE` and `HAVING`? (Hint: `HAVING` filters after `GROUP BY` — it filters *groups*, not rows.)
3. If a member has borrowed 5 books, and you JOIN members to loans, how many rows do you get for that member? Why?

## When You're Stuck

- A basic join: `SELECT books.title, members.name FROM loans JOIN books ON loans.book_id = books.id JOIN members ON loans.member_id = members.id`
- `LIKE '%word%'` matches any value containing "word". In SQLite, use `LOWER(title) LIKE '%word%'` for case-insensitive matching.
- `GROUP BY member_id HAVING COUNT(*) > 3` finds members with more than 3 loans.
- Date comparison: `WHERE borrowed_date < date('now', '-14 days')` finds loans more than 14 days old.

## Once It Works — Go Further

1. Write a query that finds the most borrowed book of all time. What does this query look like? How many JOINs does it need?
2. Write a query that finds members who have never borrowed any book (no loans in the table). This requires a `LEFT JOIN` and a `WHERE IS NULL` clause — look these up.
