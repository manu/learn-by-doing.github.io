---
title: "6.1 Why CSV Hurts"
parent: SQL as a Solution
nav_order: 1
---

# Exercise 6.1 — Why CSV Hurts

## The Story

You have measured the pain of CSV at scale. Now, before writing a single SQL query, you will articulate exactly why CSV is the wrong tool — so that every feature of SQL you learn has a clear purpose behind it.

This exercise is all writing. No code.

## What to Do

### Part A — List the specific failures

Write a numbered list of every problem you encountered with CSV storage. Be specific. Not "it was slow" — instead: "searching 100,000 records required 100,000 comparisons, taking 0.8 seconds, which is too slow when multiple users are searching simultaneously."

Aim for at least five distinct problems. Possible categories:
- Speed (search, startup)
- Memory (loading everything at once)
- Concurrency (two users modifying the file at the same time)
- Relationships (finding all books borrowed by a specific member)
- Data integrity (what stops someone from writing invalid data?)
- Transactions (what happens if the program crashes mid-write?)

### Part B — For each problem, state what you need

Next to each problem, write one sentence describing what a better system would need to do. Examples:

| Problem | What we need |
|---------|-------------|
| Full scan for every search | A way to look up books without scanning every row |
| Cannot link books to members | A way to express that a book is "borrowed by" a member |
| No protection against invalid year | A way to enforce that year is always a number |
| Crash mid-write corrupts the file | All-or-nothing writes — either the full change is saved or nothing is |

### Part C — Read these requirements back

After completing Part B, read your requirements column from top to bottom. Notice:
- "Look up without scanning" → this is what an *index* does
- "Express relationships" → this is what *foreign keys* do
- "Enforce data types" → this is what a *schema* does
- "All-or-nothing writes" → this is what a *transaction* does

SQL was designed specifically to provide these capabilities. Every SQL feature you will learn in the next four exercises exists to solve one of the problems on your list.

## Topics You Will Learn

- How to articulate a technical problem precisely
- The specific limitations of flat-file storage
- Why relational databases were invented (the actual history)
- Mapping problems to solutions before learning the solution's API

## Before You Start — Think About This

1. The CSV file has no concept of a "member". To track who borrowed a book, what would you have to do? (Add a column? Create a second CSV? What problems does each approach introduce?)
2. If two people add a book at exactly the same time — both opening the file, both reading it, both writing a new line — what might the file look like when they are done?
3. Nothing stops you from writing `year = "banana"` in the CSV. In a library of 100,000 books, how would you find and fix all the rows with invalid years?

## Once It Works — Go Further

1. Look up the history of relational databases — specifically Edgar Codd's 1970 paper that introduced the relational model. What problem was he solving? Does it match the problems on your list?
2. Try to solve the "two users at the same time" problem using only Python and CSV. Write the code. Then describe what you had to do and why it was complicated. This is the value of a tool that handles concurrency for you.
