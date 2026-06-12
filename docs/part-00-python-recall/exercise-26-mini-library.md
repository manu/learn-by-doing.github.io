---
title: "0.26 Mini Library"
parent: Python Recall Bootcamp
nav_order: 26
---

# Exercise 0.26 — Mini Library

## The Story

You have now used every building block: variables, decisions, loops, lists, dictionaries, and file reading. This exercise puts them all together into one program — the first real version of the Library Management System that will grow throughout this entire course.

The Mini Library is small by design. But even at this size, you will start to feel something: the code is getting harder to manage. A function that does too much. A file that is getting long. Logic that is repeated in two places. That feeling is not a mistake — it is the point. It is what makes Part 1 necessary.

## What to Build

A menu-driven command-line program that stores books in a CSV file called `library.csv`.

```
=== Mini Library ===
1. Add book
2. List all books
3. Search by title
4. Quit

Choose an option: 1

Title: The Alchemist
Author: Paulo Coelho
Year: 1988
Book added.

Choose an option: 2

--- All Books ---
The Alchemist by Paulo Coelho (1988)

Choose an option: 3

Search title: Alchemist
Found: The Alchemist by Paulo Coelho (1988)

Choose an option: 4
Goodbye.
```

Requirements:
- Books must be saved to `library.csv` so they survive when the program is restarted
- The CSV must be readable by a spreadsheet like LibreOffice or Excel
- Each time the program starts, it should load books from the file automatically
- Search should work even if the user types only part of the title (e.g., "Alchemy" finds "The Alchemist")

## Topics You Will Need

Everything from exercises 0.1 to 0.8:
- `input()`, `int()`, `float()`, `str()` — type conversions
- `if/elif/else` — the menu logic
- `while` loop — to keep the menu running
- Lists and dictionaries — to store books in memory
- File reading and writing — to load and save to CSV
- String methods — `.strip()`, `.split()`, `.lower()` for search

## Before You Start — Think About This

1. The program has two jobs related to the file: loading books when it starts, and saving a book when one is added. When exactly should each happen? What happens if you try to load a file that does not exist yet (first run)?
2. The menu keeps repeating until the user chooses Quit. What kind of loop suits this? What is the exit condition?
3. Search needs to find a book even when the user types only part of the title. `"Alchemist" in "The Alchemist"` is `True` in Python. How do you make this case-insensitive?
4. Before writing any code, draw the structure of your program on paper. What are the major sections? What does each section do? How do they connect?

## When You're Stuck

- Load the CSV at the start using the same pattern from Exercise 0.6. If the file does not exist, start with an empty list — use `try/except` or check with `import os; os.path.exists("library.csv")`.
- To save a book, open the file in append mode: `open("library.csv", "a")`. Write the book as a single line: `title,author,year\n`.
- The menu `if/elif` chain: check if the input is `"1"`, `"2"`, `"3"`, or `"4"`. If none match, print "Invalid option."
- For partial title search: loop through all books, and for each one check `if search_term.lower() in book["title"].lower()`.

## What to Notice When It Works

Look at your finished code. Ask yourself:
- How long is it? Could someone else read it and understand it immediately?
- Is there any code that appears twice, doing nearly the same thing?
- If you wanted to add a 5th menu option — "Edit book details" — how hard would that be?
- If you wanted to change the CSV format from commas to tabs, how many places in the code would you need to change?

Write down your answers. These observations are the starting point for Part 1.

## Transition

This is the last exercise of Part 0. The Mini Library works — but it has problems. Those problems are not bugs. They are design problems. Part 1 begins because the code is ready to be improved.
