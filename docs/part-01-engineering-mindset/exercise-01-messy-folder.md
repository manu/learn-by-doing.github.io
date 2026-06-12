---
title: "1.1 Messy Folder"
parent: Engineering Mindset
nav_order: 1
---

# Exercise 1.1 — Messy Folder

## The Story

After finishing the Mini Library, your project folder looks like this:

```
my stuff/
    library.py
    library2.py
    library_v2.py
    library_new.py
    library_FINAL.py
    library_FINAL2.py
    test.py
    testing.py
    temp.py
    books.csv
    books_backup.csv
    books2.csv
    notes.txt
    notes2.txt
    README (copy).txt
```

You come back to this folder two weeks later. You cannot remember which file is the real one. You do not know what `temp.py` does. You do not know which CSV is the correct one. You cannot find your notes.

This is not a Python problem. This is an *engineering* problem.

## What to Think About

Before this exercise gives you anything to do, answer these questions honestly:

1. How long would it take you to find the correct version of `library.py` right now?
2. If a friend wanted to use your library program, what would you tell them to run?
3. If you added a new feature today, which file would you edit?
4. Why did you name files `_new`, `_v2`, `_FINAL`, `_FINAL2`? What problem were you trying to solve when you did that?

## What to Do

### Part A — Clean the folder

Reorganize the folder. You decide the structure, but it must satisfy these rules:

- Someone who has never seen your project can immediately tell what file to run
- Old versions are clearly separated from the current version (or deleted entirely)
- Data files are not mixed in with program files
- Notes are in one place with a clear name

There is no single correct answer. But you must be able to *explain* every decision you made.

### Part B — Write a README

Create a file called `README.txt` (or `README.md`) in the top level of the folder. It must answer:

1. What does this program do?
2. How do I run it?
3. What do I need to have installed before I can run it?
4. What files does the program create or need?

Write it as if you are writing for someone who has never met you. Write one sentence per answer — do not write paragraphs.

### Part C — Naming Audit

Look at every variable name in your `library.py`. For each one, ask:
- Does the name tell me what the variable holds?
- Would someone reading this for the first time understand immediately?

Rename any variable that does not pass this test. Examples of bad names: `x`, `temp`, `data`, `lst`, `val`, `thing`. Examples of better names: `books`, `member_name`, `search_term`, `total_count`.

## Topics You Will Learn

- Folder structure and project organization
- README conventions
- Naming variables, files, and functions clearly
- The concept of *information architecture* — making information easy to find

## Before You Start — Think About This

1. What is the difference between a name that describes *what something is* versus one that describes *what you did to it* (`books` vs `new_books`)?
2. A README is not documentation of every line of code. It is the answer to: "What do I need to know to *use* this?" What is the minimum a user needs to know?
3. Folder structure is a form of communication. It tells a reader: "these things belong together, those things are separate." What groupings make sense for a library project?

## Once It Works — Go Further

1. Look at any popular open-source project on GitHub (for example: `requests`, `flask`, or `numpy`). Study their folder structure and README. What do they have that yours does not?
2. Write a one-paragraph "architecture note" — a plain-English description of how your Mini Library works: what the files are, what each one does, and how they connect.
