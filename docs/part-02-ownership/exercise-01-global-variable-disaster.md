---
title: "2.1 Global Variable Disaster"
parent: Ownership and Responsibility
nav_order: 1
---

# Exercise 2.1 — Global Variable Disaster

## The Story

A student built a version of the Mini Library using global variables for everything. The program mostly works — but strange things happen:

- Adding a book sometimes changes the search results unexpectedly
- Running a search twice in a row gives different results
- A function that should only display data is somehow modifying the list

The student cannot figure out why. The program looks correct line by line, but it breaks in ways that are hard to predict.

The problem is not a bug in any single line. The problem is the *design*. When every function can read and change the same global variables, you can never be sure what any one function does — because any function might have silently changed something.

## Read This Code First

Study this program before doing anything else:

```
books = []
last_search = ""
total_added = 0

def add_book():
    title = input("Title: ")
    author = input("Author: ")
    books.append({"title": title, "author": author})
    total_added = total_added + 1
    print("Added.")

def search():
    last_search = input("Search: ")
    for book in books:
        if last_search in book["title"]:
            print(book["title"])

def show_stats():
    print("Books in library:", len(books))
    print("Last search was:", last_search)
    print("Total ever added:", total_added)

while True:
    choice = input("1=Add 2=Search 3=Stats 4=Quit: ")
    if choice == "1":
        add_book()
    elif choice == "2":
        search()
    elif choice == "3":
        show_stats()
    elif choice == "4":
        break
```

## What to Do

### Part A — Find the bugs

Run the program. Try adding a book, searching, and checking stats. You will encounter at least two errors and one silent bug (a bug that does not crash the program but gives wrong results).

For each problem you find, write down:
1. What you did that caused it
2. What the program did (or said)
3. Why you think it happened

### Part B — Understand why

Before fixing anything, answer these questions in writing:

1. `add_book()` tries to do `total_added = total_added + 1`. Python raises an error. Why? (Hint: Python sees `total_added` on the right side of `=` before the left side is assigned. Is it reading the global or creating a local?)
2. After you call `search()`, the global `last_search` is not updated. Why not? What did the function actually update?
3. `show_stats()` shows `0` for `total_added` even after books are added. Why?

### Part C — Fix it properly

Rewrite the program so that:
- Functions receive the data they need as *parameters*
- Functions return values instead of modifying globals
- The only place where the list is managed is the main loop
- No function reads or writes a global variable

Your rewritten program should produce identical behaviour to the original — but the *design* will be completely different.

## Topics You Will Learn

- Global vs local scope — what a variable's *scope* means
- Why functions that rely on globals are unpredictable
- Passing data into functions with parameters
- Returning data out of functions with `return`
- The principle: a function should be predictable — given the same inputs, it always does the same thing

## Before You Start — Think About This

1. If a function can read *and modify* any global variable, how many places in the entire program could be responsible for changing that variable? Why is that a problem when you are debugging?
2. A well-designed function takes inputs (parameters) and produces an output (return value). It should not reach outside itself to grab data, and it should not modify things outside itself as a side effect. Does `add_book()` in the broken version satisfy this description?
3. If someone handed you the function `add_book()` without showing you the rest of the program, could you tell what it does just by reading it? Why or why not?

## Once It Works — Go Further

1. Look at your Mini Library from Part 0. Does it have any global variables? If so, apply the same fix — pass data in, return it out.
2. Write a version of `search()` that *returns* a list of matching books instead of printing them. Then have the caller decide how to display them. Why is this more flexible?
