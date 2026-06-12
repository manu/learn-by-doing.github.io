---
title: "6.3 Create Tables and Migrate Data"
parent: SQL as a Solution
nav_order: 3
---

# Exercise 6.3 — Create Tables and Migrate Data

## The Story

You have a schema design. Now you will create the actual database and move your 10,000 books from CSV into SQLite.

SQLite is a database engine that stores everything in a single file — perfect for a project that runs on one machine. It is used in Android, iOS, Firefox, and thousands of other applications. It is a real database, not a toy.

## What to Do

### Step 1 — Create the database

Write a Python script called `create_db.py`. It should:
1. Connect to a new SQLite file: `library.db`
2. Create the `books`, `members`, and `loans` tables using the schema from Exercise 6.2
3. Close the connection

Run it. A file called `library.db` will appear in your project folder.

You can inspect it using a free tool called **DB Browser for SQLite** (download at `sqlitebrowser.org`). Open `library.db` — you should see your three empty tables.

### Step 2 — Migrate the books

Write a second script called `migrate.py`. It should:
1. Read all rows from `library.csv`
2. Connect to `library.db`
3. For each book row, insert a record into the `books` table
4. Commit and close

The Python `sqlite3` module is built in — no installation needed.

After running the migration, open DB Browser and look at the `books` table. You should see 10,000 rows.

### Step 3 — Update the library program

Now update `storage.py` (or `library.py`) to use the database instead of the CSV:
- Replace `load_books()` — instead of reading a CSV, run a `SELECT` query
- Replace `save_book()` — instead of appending to a CSV, run an `INSERT` query

The interface and the rest of the program should not change at all.

### Step 4 — Measure startup time again

Run the program and time the startup. Compare it to your measurements from Part 5.

Loading 10,000 rows from SQLite should be significantly faster than reading and parsing a CSV — even before adding any indexes.

## Topics You Will Need

- Python's `sqlite3` module: `connect()`, `cursor()`, `execute()`, `fetchall()`, `commit()`, `close()`
- `CREATE TABLE` SQL statement
- `INSERT INTO` SQL statement
- `SELECT * FROM` SQL statement
- `with` statement for database connections (ensures cleanup even on errors)

## Before You Start — Think About This

1. Why do you write a separate migration script instead of building migration logic into the main program? (Think: what happens if migration runs twice?)
2. The migration must insert 10,000 rows. Should you commit after each `INSERT`, or commit once after all inserts? What is the difference in speed and safety?
3. After migration, you have two sources of truth: `library.csv` and `library.db`. Which one should the program use going forward? What do you do with the old CSV?

## When You're Stuck

- `conn = sqlite3.connect("library.db")` opens (or creates) the database file.
- `cursor = conn.cursor()` gives you an object to run queries.
- `cursor.execute("INSERT INTO books (title, author, year) VALUES (?, ?, ?)", (title, author, year))` inserts one row. The `?` placeholders are important — do not use string formatting here (you will learn why in Part 8).
- `conn.commit()` saves all pending changes. Without this, inserts are not saved.

## Once It Works — Go Further

1. Open the database in DB Browser and manually insert a row with an invalid year (a word instead of a number). Does SQLite accept it? What does this tell you about SQLite's type enforcement? (Look up "SQLite type affinity" — it is an unusual design choice.)
2. What happens if you run `migrate.py` twice? Write a check that prevents duplicate insertion.
