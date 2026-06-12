---
title: "4.3 Split into Modules"
parent: Refactoring
nav_order: 3
---

# Exercise 4.3 — Split into Modules

## The Story

Even after extracting functions, everything still lives in one file. As the library grows, this becomes a problem: the file that handles the menu also knows about CSV storage. The search function is in the same file as the display code. Changing how books are stored means reading through menu logic to find the relevant lines.

Modules solve this by grouping related functions into separate files. Each file has a clear responsibility. When you want to change storage, you open `storage.py`. When you want to change the menu, you open `menu.py`. The rest of the program does not need to know or care about those details.

This is called *separation of concerns* — and it is one of the most fundamental principles in software design.

## What to Do

### Step 1 — Identify the three concerns

Your library program currently has three distinct concerns:

1. **Storage** — reading from and writing to `library.csv`
2. **Books** — the logic for searching, filtering, and validating book data
3. **Interface** — displaying the menu, reading user input, printing results

These three concerns should live in three files.

### Step 2 — Create the module files

Create three new Python files in your project folder:
- `storage.py` — will contain `load_books()` and `save_book()`
- `books.py` — will contain `search_books()`, `add_book()`, and any book-related logic
- `interface.py` — will contain `show_menu()`, `get_user_choice()`, `print_book_list()`

Move the relevant functions from `library.py` into each file. Then import them back in `library.py`:

```
from storage import load_books, save_book
from books import search_books
from interface import show_menu, print_book_list
```

### Step 3 — Verify with each move

After moving each function, run the program. Do not move everything at once and then try to fix all the errors simultaneously.

### Step 4 — Read `library.py` after the split

The main file should now read as a clean orchestration of the three modules. It should import what it needs, and call functions. No storage logic. No display logic. No book logic. Just coordination.

## What to Observe

Open any one module — say, `storage.py`. Notice that it knows nothing about the menu, and nothing about book validation. It only knows how to read and write CSV. If you later decide to switch from CSV to a database, you only change `storage.py`. Nothing else in the program needs to change.

This property — the ability to change one part without touching the rest — is what makes modular code worth the effort.

## Topics You Will Learn

- Python modules and `import` statements
- `from module import function` vs `import module`
- Separation of concerns
- How module boundaries reduce the ripple effect of changes

## Before You Start — Think About This

1. If `storage.py` needs to know the filename `library.csv`, where should that value live? In `storage.py`? In `library.py`? As a constant at the top of whichever file you put it in?
2. Can `books.py` import from `storage.py`? Can `storage.py` import from `books.py`? What happens if two modules import from each other (a *circular import*)? How do you avoid it?
3. A module should have a single clear responsibility that you can describe in one noun: "storage", "books", "interface". If you cannot describe the responsibility in one noun, the module is doing too much.

## When You're Stuck

- Move one function at a time. After each move, run the program. This makes errors easy to trace — if something breaks, you know which move caused it.
- If a function in `books.py` needs access to storage, pass the books list as a parameter rather than importing storage directly from books.
- `import error: cannot import name 'X'` means the function `X` either does not exist in the module you are importing from, or there is a typo. Check spelling and check that the function is at the top level (not indented inside another function).

## Once It Works — Go Further

1. Add a fourth module: `config.py`, containing only constants — the filename, the CSV column order, the pass mark for the quiz. Then import these constants into the modules that need them. This way, if you ever want to change the filename, you change it in one place.
2. Count the lines in each module after the split. If one module is much longer than the others, investigate why — it may be doing more than its fair share.
