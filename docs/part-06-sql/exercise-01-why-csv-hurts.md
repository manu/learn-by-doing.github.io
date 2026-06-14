---
title: "6.1 Why CSV Hurts"
parent: SQL as a Solution
nav_order: 1
---

# Exercise 6.1 — Why CSV Hurts

## The Story

The library has 10,000 books in a CSV file. You have measured how slow it is. You have seen it break when two people use it at the same time. You discovered that tracking loans would require a second CSV — and linking the two would mean scanning both files every time.

Now, before writing a single line of SQL, you need to do something harder: put the pain into words.

The librarian is meeting with the school's IT committee next week. She wants to replace the CSV system with a proper database. The committee will ask: "Why? What is wrong with the current system?"

She turns to you. "Can you write it up for me?"

This is a writing exercise. No code.

## What to Do

### Part A — List the failures

Write a numbered list of every problem you discovered with the CSV system. Be specific about each failure. Not "it was slow" — but "searching 10,000 books required checking every book one by one, taking 0.8 seconds — and that time grows as books are added."

Aim for at least five distinct problems. Think across these areas:
- Speed (startup, search, what happens at 100,000 books)
- Memory (how much is loaded, and whether that is sustainable)
- Simultaneous use (what happened when two windows were open at once)
- Relationships (how would you track loans? what would the second CSV look like?)
- Data integrity (what stops someone from entering an invalid year, or a blank title?)
- Crash safety (what happens if the program crashes while writing a new book?)

### Part B — For each failure, write what you need

Next to each problem, write one sentence describing what a better system would need to provide.

| Problem | What we need |
|---------|-------------|
| Full scan for every search | A way to locate books without checking every row |
| Crash mid-write corrupts the file | Either the write fully completes, or nothing changes |
| Two CSV files needed for loans | A way to link records across tables without copying data |
| Nothing prevents `year = "banana"` | Rules that reject invalid data before it is saved |

Add your own rows for each problem you found.

### Part C — Keep the list

Read your requirements column from top to bottom. This is your specification — a precise description of what a better storage system must do.

Save this document. After each exercise in Part 6, return to it and check whether that exercise solved one of your requirements. By the end of Part 6, every requirement should be answered.

## Before You Start — Think About This

1. The CSV file has no concept of a "member". To track who borrowed a book, what would you have to add? A new column in `library.csv`? A second file? Walk through the design and write down every new problem that approach creates.
2. If two programs open the same CSV file at the same time — both read it, both modify it, both write it back — what happens? Which write survives? Is there a version where neither does?
3. The library needs to check whether a book is already borrowed before lending it again. With CSV, how many file reads does that check require? Write the steps.

## When You're Stuck

- The problems are not just "it was slow." Each problem has a specific cause. "Startup is slow because the program loads every book into memory even when the user only wants to search one title" is a useful observation. "It was slow" is not.
- For the crash-safety problem: think about what a CSV write looks like physically. You open the file, you write all 10,000 rows, you close it. What happens if the power goes out at row 5,000?
- For the relationship problem: imagine a real paper-based library. When a student borrows a book, what information do you write down, and where?

## Once It Works — Go Further

1. Look up the history of relational databases. Edgar Codd wrote a paper in 1970 called "A Relational Model of Data for Large Shared Data Banks." What problem was he solving? Does it match your list?
2. Try to solve the simultaneous-write problem using only Python and CSV. What would you have to build? (Think: file locking, waiting, retrying.) Write a paragraph describing what you would need to implement. This is what a database provides automatically.
