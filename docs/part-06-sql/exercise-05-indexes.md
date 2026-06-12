---
title: "6.5 Indexes"
parent: SQL as a Solution
nav_order: 5
---

# Exercise 6.5 — Indexes

## The Story

Your library database has 10,000 books. The search query `SELECT * FROM books WHERE title LIKE '%mystery%'` works — but how fast? And what happens with 1,000,000 books?

Without an index, every `SELECT` query with a `WHERE` clause must scan every row in the table — exactly the same problem you had with CSV. The database is smarter and faster than a Python list scan, but the fundamental algorithm is the same: check every row.

An index is a separate data structure that the database maintains automatically. It makes certain queries dramatically faster by allowing the database to jump directly to relevant rows — like an index in the back of a textbook, versus reading every page to find a word.

## What to Do

### Step 1 — Measure search time without an index

Write a Python script that runs the same title search 100 times and measures the average time:

```
Run: SELECT * FROM books WHERE title LIKE '%history%'
Repeat 100 times
Calculate average time per query
```

Record the number.

### Step 2 — Create an index

```
CREATE INDEX idx_books_title ON books (title);
```

Run this once in DB Browser or in a Python script.

### Step 3 — Measure again

Run the same 100-query test. Record the new average time.

Calculate the speedup: `old_time / new_time`. Write down what you observe.

### Step 4 — Understand the trade-off

Indexes are not free. Answer these questions by experimenting:

1. After creating the index, how much larger is `library.db`? (Check the file size before and after.)
2. Insert 1,000 new books into the database — once with the index present, once after dropping it. Which is faster? By how much?
3. Why would every index you create slow down writes but speed up reads?

### Step 5 — Decide which columns need indexes

Look at your library queries from Exercise 6.4. For each query, decide:
- Which column(s) does the `WHERE` clause filter on?
- Would an index on that column help?
- Is this query run often enough to justify the storage and write cost?

Create indexes for the columns that deserve them.

## Topics You Will Learn

- `CREATE INDEX` and `DROP INDEX`
- Why indexes speed up reads and slow down writes
- Which queries benefit from indexes and which do not
- The trade-off between read performance and storage space
- Why `LIKE '%word%'` (leading wildcard) cannot use a standard index

## Before You Start — Think About This

1. An index in a book lets you find pages about "photosynthesis" without reading every page. How is a database index similar? What is it storing internally? (Look up "B-tree index.")
2. If you add an index on `title`, does a query filtering by `author` become faster? Why not?
3. `LIKE '%history%'` (wildcard on both sides) cannot use a standard index because the database does not know which part of the title to look up. `LIKE 'history%'` (wildcard only at the end) *can* use an index. Why is this?

## When You're Stuck

- `EXPLAIN QUERY PLAN SELECT ...` in SQLite shows whether a query uses an index or does a full table scan. Run this before and after creating an index to confirm the index is being used.
- If your LIKE query has a leading wildcard (`%word`), an index on that column will not help. Full-text search requires a different data structure — look up SQLite FTS5.
- Indexes are automatically updated when rows are inserted, updated, or deleted. You do not maintain them manually.

## Once It Works — Go Further

1. Look up *compound indexes* (indexes on more than one column). Create a compound index on `(author, year)`. What queries does this help? What queries does it not help?
2. Using your measurements from this exercise and Part 5, build a table showing:
   - CSV search time at 10,000 rows
   - SQLite search without index at 10,000 rows
   - SQLite search with index at 10,000 rows

   This table is a concrete demonstration of why the architecture changed.
