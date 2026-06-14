---
title: "6.5 Indexes"
parent: SQL as a Solution
nav_order: 5
---

# Exercise 6.5 — Indexes

## The Story

The librarian has been using the new database for a week. She is pleased. But she comes back with a complaint on Friday: "Searching by author name takes a long time. Searching by title is fast. Why are they different?"

You check. She is right. A search by title returns quickly. A search by author name takes noticeably longer. Both are simple `WHERE` clauses. Both search the same table. What is different about them?

You have not yet told the database anything about which fields you plan to search often. As far as the database is concerned, all columns are equal — which means it searches all of them the same way: by checking every row.

When you moved from CSV to SQLite, you assumed the database would be faster. It is. But without any guidance about how the data will be used, the database is still reading every row for every search — the same fundamental problem as before.

This exercise is about giving the database that guidance.

## What to Do

### Part A — Confirm the problem

Write a small measurement script that runs the same author-name search 100 times and records the average time per search. Run the same test for a title search.

Record both numbers. Which is slower? Is the difference consistent across multiple runs?

### Part B — Understand why

Before creating any index, answer these questions in writing:
- Without any additional structure, how does the database find all books by "Ruskin Bond"? How many rows does it check?
- The title search was fast. Did you add anything to the `title` column that the `author` column does not have? Look back at your schema from Exercise 6.2.
- Think of a physical library. If you needed to find all books by a specific author quickly, what physical tool would you add to the library? How would it be organised?

### Part C — Create an index and measure again

An index is a separate structure that the database maintains alongside the table. It allows certain searches to jump directly to matching rows instead of checking every row.

Look up how to create an index in SQLite. Create one on the `author` column. Then run your measurement script again.

Record:
- The search time before the index
- The search time after the index
- How much faster is it? Express this as a ratio.

Check the file size of `library.db` before and after. How much larger did the index make the database?

### Part D — Understand the cost

Indexes are not free. Design an experiment to measure the impact on writes:
- Insert 1,000 books into the database with the index present
- Drop the index, then insert another 1,000 books without it
- Measure both

Which insert was faster? By how much?

Now explain in writing: why does an index slow down writes? Where does the extra time go?

### Part E — Decide which columns need indexes

Look at all the queries you wrote in Exercise 6.4. For each query, identify which column the `WHERE` clause filters on. Then decide: does this column deserve an index?

Write your reasoning for each decision. Some columns are searched frequently — they deserve indexes. Some are almost never searched — adding an index would slow down writes for no benefit.

Create indexes for the columns you decided deserve them.

## Before You Start — Think About This

1. Think of an index in the back of a textbook. How does it let you find pages about "photosynthesis" without reading every page? What does it store, and how is it organised? How is a database index similar?
2. If you add an index on `title`, does a search by `author` become faster? Why not?
3. Consider two searches: `WHERE title LIKE 'history%'` (starts with "history") versus `WHERE title LIKE '%history%'` (contains "history" anywhere). Only one of these can use a standard index. Which one? Why?

## When You're Stuck

- After creating an index, you can verify whether the database actually uses it by running `EXPLAIN QUERY PLAN` before your `SELECT` statement. The output will say whether it did a full table scan or used the index.
- If your search uses a leading wildcard — `LIKE '%word%'` — a standard index cannot help, because the database does not know where in the title to start looking. Look up "SQLite FTS5" for a different approach to full-text search.
- Indexes are maintained automatically. When you insert, update, or delete a row, every index on that table is updated too. That is the write cost.

## Once It Works — Go Further

1. Look up *compound indexes* — indexes that cover more than one column. Create one on `(author, year)`. Which queries does it help? Which queries does it not help? Why?
2. Build a summary table using your measurements across Part 5 and Part 6:

   | Method | Search time |
   |--------|------------|
   | CSV, 10,000 rows | |
   | SQLite without index | |
   | SQLite with index | |

   This is your complete picture of how the architecture evolved and why.
