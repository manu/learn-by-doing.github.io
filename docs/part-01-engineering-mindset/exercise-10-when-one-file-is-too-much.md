---
title: "1.10 When One File Is Too Much"
parent: Engineering Mindset
nav_order: 10
---

# Exercise 1.10 — When One File Is Too Much

## The Story

Every project starts as one file. That is the right place to start.

But then something happens:

- You add member management. The file grows to 150 lines.
- You add a CSV export feature. The file grows to 230 lines.
- You add search history. The file grows to 310 lines.
- You add input validation everywhere. The file grows to 450 lines.

Now try to find where the search function is. Scroll. Scroll more. Is it above or below the validation code? Which variables does it use? Does it depend on the member code or only the book code?

A 450-line file is not a size problem — it is a *navigation* problem and a *dependency* problem. When everything is in one place, everything can affect everything else. You change one line and something unrelated breaks.

The moment a file becomes hard to navigate, it is time to split it.

## What to Do

### Part A — Map what your file contains

Open your `library.py` (or `src/library.py` after Exercise 1.7). Read through it completely. Make a list of every function and group them by what they are about:

- Functions that deal with books (adding, removing, searching)
- Functions that deal with files (reading CSV, writing CSV)
- Functions that deal with user interaction (printing menus, reading input)
- Functions that deal with data validation (checking year is a number, title is not empty)
- Anything else?

Write this grouping down. You are mapping the hidden structure inside the file.

### Part B — Design the split

Now design what the file layout would look like if each group had its own file. For each file you design, write:
- The filename (e.g., `books.py`, `storage.py`, `ui.py`)
- What it contains (list the functions)
- What it needs from other files (what would it have to import?)

Draw arrows from each file to the files it depends on. Which file is at the center — the one everything else depends on?

This drawing is called a **dependency diagram**. You will use this concept throughout the curriculum.

### Part C — Recognize the signals

Here are signals that a file is ready to split. For each signal, find an example (or lack of example) in your own Mini Library:

| Signal | What it looks like |
|--------|--------------------|
| More than 200 lines | You scroll constantly to find functions |
| Mixed responsibilities | CSV reading sits next to menu printing |
| Hard to name | The file is called `library.py` but it handles users too |
| "Hidden coupling" | Changing the CSV format breaks the display code |
| Repeated imports | The same `import csv` and `import os` appear in multiple places of the same file (a sign of repeated work) |

For each signal, write: does your file have this problem? Give a specific example.

### Part D — (Optional) Execute the split

If your file has grown large enough, split it into the files you designed in Part B. After the split:
- Each file must import what it needs from the others
- The program must run exactly as before (no behavior change)
- Test every feature manually after the split

If your file is still small (under 150 lines), skip Part D — the cost of splitting is not worth the benefit yet. Document this decision: "Not splitting because the file is still small enough to navigate easily."

## Topics You Will Learn

- How to recognize when a file has become too large to navigate
- The concept of separation of concerns at the file level
- What a dependency diagram is and why engineers draw them
- The principle that splitting should be motivated by real pain, not by a rule

## Before You Start — Think About This

1. You could split a 50-line file into five 10-line files. Should you? What would you gain and what would you lose?
2. If you split `library.py` into `books.py` and `storage.py`, and `books.py` needs to use functions from `storage.py`, how does Python let one file use code from another?
3. What is the difference between "this code is related to books" and "this code depends on books"? Why does the distinction matter when designing file splits?

## When You're Stuck

- In Python, a function in `storage.py` can be used in `books.py` with `from storage import save_to_csv`.
- The most common mistake when splitting files is creating a circular import: `books.py` imports from `storage.py`, and `storage.py` imports from `books.py`. This causes Python to fail at startup. Look for this before you split.
- When in doubt, keep things together a little longer. A premature split creates complexity without benefit. The right time to split is when navigation or testing becomes painful.

## Once It Works — Go Further

1. After splitting, run your program and test all features. Write down whether the split made the code easier or harder to work with. Be honest — splitting is not always an improvement.
2. In Part 4 of this curriculum, you will do this at a much larger scale — a 500-line file with deep interdependencies. The dependency diagram you drew in Part B of this exercise is the same technique you will use there. Keep it.
