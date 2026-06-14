---
title: "6.3 Create Tables and Migrate Data"
parent: SQL as a Solution
nav_order: 3
---

# Exercise 6.3 — Create Tables and Migrate Data

## The Story

The design is on paper. Three tables, columns listed, connections drawn. Now comes the first real question: how do you actually build this, and how do you move the 10,000 books already in the CSV into the new database without losing any of them?

The librarian is watching. She needs the system working by Monday. If the migration fails partway through — say, it crashes after loading 6,000 of the 10,000 books — is the data safe? Or is the database now half-full, with no way to tell which books made it across?

You have three separate problems to solve:
1. Create the database with the correct structure
2. Move the existing 10,000 books across, safely
3. Update the library program so it reads from the database instead of the CSV

## What to Do

### Part A — Build the database

SQLite is a database engine that stores everything in a single file — perfect for a project that runs on one machine. Python includes a `sqlite3` module built in, with no installation needed.

Write a Python script called `create_db.py`. Its only job is to create the database file (`library.db`) and create the three tables based on your design from Exercise 6.2. Nothing else.

Run it. Open the file in **DB Browser for SQLite** (a free tool at `sqlitebrowser.org`). You should see your three empty tables with the correct columns.

Do not move on until the structure looks exactly like your paper design.

### Part B — Migrate the books

Write a separate script called `migrate.py`. Its job is to read every book from `library.csv` and insert it into the `books` table in the database.

Before writing any code, think through these questions:
- The migration inserts 10,000 rows. Should it commit after every single insert, or once after all 10,000? What is the difference if the script crashes at row 5,000?
- Some rows in the CSV might have missing titles or invalid years. What should the migration do with those rows?
- What happens if `migrate.py` is run a second time by mistake? Would it create 20,000 rows?

Write the script, run it, and then open DB Browser to verify: the `books` table should contain exactly 10,000 rows.

### Part C — Switch the library program

Now update the library program to use the database instead of the CSV file. The goal is that nothing visible to the librarian changes — the same menu, the same search results — but the underlying storage is now the database.

Find the two places in the program that deal with storage:
- Where books are loaded at startup
- Where a new book is saved

Replace each with a database query instead of a file operation. The rest of the program should not need to change.

### Part D — Measure startup time again

Time how long the library takes to start up with the database. Compare this to your measurement from Part 5 with the CSV.

Write down both numbers. What changed, and why?

## Before You Start — Think About This

1. Why is the migration a separate script rather than a button inside the library program? What would go wrong if the migration logic ran every time the program started?
2. When migrating 10,000 rows, should you save your progress after every single book, or once at the very end? What are the trade-offs?
3. After migration, you have two copies of the books: `library.csv` and `library.db`. The program now uses only one of them. What should you do with the other? What risk comes from keeping both?

## When You're Stuck

- Python's built-in `sqlite3` module lets you connect to a database file, run SQL statements, and save (commit) your changes. Look up `sqlite3.connect`, `cursor.execute`, and `conn.commit` in the Python documentation.
- When inserting data from a variable, use `?` placeholders in the SQL string — do not build the SQL by joining strings together. You will learn exactly why this matters in Part 8.
- A database connection is a resource that needs to be closed. Using a `with` statement ensures the connection is always closed, even if the script crashes partway through.

## Once It Works — Go Further

1. Open `library.db` in DB Browser and manually insert a book where the year is a word instead of a number. Does SQLite reject it? Look up "SQLite type affinity" to understand why SQLite's type enforcement is unusual compared to other databases.
2. Run `migrate.py` a second time. What happens? How would you change the script to detect and skip books that are already in the database?
