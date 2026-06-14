---
title: "0.11 Your Own Module"
parent: Python Recall Bootcamp
nav_order: 11
---

# Exercise 0.11 — Your Own Module

## The Story

The library program has been growing exercise by exercise. By now, `library.py` has functions for reading books, searching, displaying, calculating due dates, and picking recommendations. It is getting long.

The librarian asks you to add member management — keeping track of who has a library card. You open `library.py`. It is already 80 lines. You scroll through looking for where to add the new code. You are not sure whether a function you need is at the top or the bottom.

This is the problem that modules solve — not just Python's built-in ones, but *your own*.

A module is just a Python file. When you put related functions into their own file, the code becomes easier to find, easier to change, and easier to reuse. The library can have `books.py` for book functions, `members.py` for member functions, and a main `library.py` that imports from both.

## What to Do

### Part A — Split the program

Take the library program you have built so far and split it into two files:

**`books.py`** should contain all functions that deal with books:
- Reading books from the CSV file
- Searching for a book by title
- Displaying the book list
- Picking a random recommendation

**`library.py`** should be the main program — the one the user runs. It should import from `books.py` and use those functions.

The program should behave identically to before. The only difference is how the code is organized.

### Part B — Add a members module

Create a new file called `members.py`. Add these functions:
- `add_member(name, email)` — adds a new library member to a list
- `find_member(name)` — searches for a member by name
- `list_members()` — displays all current members

Update `library.py` to import from `members.py` as well, and add a "Members" option to the menu.

### Part C — Understand what you built

Answer these questions in writing:
1. When `library.py` runs `import books`, where does Python look for `books.py`?
2. What is the difference between `import books` and `from books import search_books`? When would you use each?
3. If you change a function inside `books.py`, does `library.py` need to be changed too — or does it automatically use the updated version?
4. A function in `books.py` cannot see variables defined in `library.py`, and vice versa — unless you pass them as arguments. Why is this a good thing?

## Topics You Will Need

- Creating a `.py` file as a module — there is nothing special to do; any `.py` file is a module
- `import books` — import the whole module; call functions with `books.search_books(...)`
- `from books import search_books` — import one function directly; call it as `search_books(...)`
- `from books import search_books, list_books` — import multiple names at once
- Understanding that each module has its own namespace — its own separate space for variable names

## Before You Start — Think About This

1. Both `library.py` and `books.py` will be in the same folder. Does the folder location matter for `import` to work?
2. If `books.py` has a line at the top that reads the CSV and stores books in a variable, what happens when `library.py` imports `books`? Does the CSV get read at import time?
3. What would happen if two of your files both defined a function called `search()`? Would they conflict? Why or why not?

## When You're Stuck

- Put both files in the same folder. `import books` works when the files are side by side.
- After `import books`, you call a function as `books.function_name()`. The module name acts like a prefix.
- After `from books import search_books`, you call it as just `search_books()` — no prefix. But if `library.py` also had a function called `search_books`, there would be a conflict.
- If Python says `ModuleNotFoundError: No module named 'books'`, check that both files are in the same folder and that the filename is exactly `books.py`.

## Once It Works — Go Further

1. Create a third module: `reports.py`. Move the due-date calculator and overdue checker from Exercise 0.10 into it. Import and use them from `library.py`. You now have a program split across four files — each with a clear, single purpose.
2. Add `__name__ == "__main__"` to `books.py` — look up what this does and why it matters when a module is both imported and run directly.
