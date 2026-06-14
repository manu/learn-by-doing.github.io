---
title: "1.7 Standard Project Layout"
parent: Engineering Mindset
nav_order: 7
---

# Exercise 1.7 — Standard Project Layout

## The Story

Open any popular Python project on GitHub — Flask, Requests, Django — and you will notice something surprising. They all look almost the same. The folders have the same names. The files are in the same places. There is always a README at the top. There is always a folder for tests. There is always a folder for the actual code.

This is not an accident. The Python community settled on a standard layout because it solves a recurring problem: when everyone organizes projects differently, every project you join requires learning its layout before you can start. A standard layout means you can navigate an unfamiliar project in minutes.

Here is what that standard layout looks like for a small project:

```
mini-library/
├── README.md
├── requirements.txt
├── src/
│   └── library.py
├── data/
│   └── books.csv
├── tests/
│   └── test_library.py
└── docs/
    └── how-it-works.md
```

Each folder has one job:
- `src/` — the source code, the actual program
- `data/` — files the program reads and writes (CSVs, databases, logs)
- `tests/` — programs that check whether the code works correctly
- `docs/` — documentation beyond the README

## What to Do

### Part A — Understand before you reorganize

Before moving any files, answer these questions about your current Mini Library:

1. Where is the code that runs when you type `python library.py`?
2. Where is the data the program reads (the CSV)?
3. Do you have any files that test the program? If not, what would you test?
4. Is there any documentation beyond the README?

Write one sentence for each answer. This is your current state.

### Part B — Design your new layout

On paper (not on the computer yet), draw the folder structure you will use for the Mini Library. It must:
- Follow the standard layout described above
- Have a place for every file that currently exists in your project
- Have a place for every file you might create in the future (logs, a database, more documentation)

Write one sentence for each folder explaining what belongs there and what does not.

### Part C — Migrate the project

Now move your files into the new structure. After the move:
- Your program must still run (you may need to update file paths inside the code)
- The README must still point to the correct files
- Nothing should be deleted — only moved

Test the program after the migration. If it breaks, fix the path references inside the code.

### Part D — Why `requirements.txt`?

Create a file called `requirements.txt` in the root of your project. Right now it may be empty (the Mini Library uses only standard library modules). But answer this: what would go in this file if your project used a library someone else wrote? Why is it useful to list dependencies in a file rather than just telling people verbally?

## Topics You Will Learn

- Standard Python project layout (`src/`, `data/`, `tests/`, `docs/`)
- The concept of convention over configuration — agreeing on a layout so teams can navigate quickly
- How file paths inside code must change when files move
- What `requirements.txt` is for

## Before You Start — Think About This

1. Why does source code go in `src/` instead of just in the root folder? What problem does that separation solve?
2. The `data/` folder might contain files that change every time the program runs (like a CSV of books). Should those files be included when you share the code with someone? Why or why not?
3. If you have a `tests/` folder but no tests yet, is there value in having the empty folder? What message does it send to someone looking at your project?

## When You're Stuck

- If the program breaks after moving files, the most likely cause is a file path: `open("books.csv")` needs to become `open("data/books.csv")` after the move.
- Start by moving one file at a time. Test after each move. Don't move everything at once.
- Look at the GitHub repository for the `requests` library. Notice what folders exist and which files are at the root level. You don't need to understand the code — just study the layout.

## Once It Works — Go Further

1. Look at three real Python projects on GitHub. Make a table: what folders does each one have? What is the same across all three? What is different? What do the differences tell you about the project?
2. Some large projects have a `scripts/` folder containing small utility programs that aren't part of the main code. Why might you separate these from `src/`? Can you think of a script your Mini Library might eventually need?
