---
title: "0.9 Search and Skip"
parent: Python Recall Bootcamp
nav_order: 9
---

# Exercise 0.9 — Search and Skip

## The Story

The library has a list of books that were returned today. The librarian has two tasks:

**Task 1 — Find the first damaged book.**
Go through the returned books one by one. The moment you find a damaged one, stop and report it. There is no point checking the rest — the librarian will deal with one at a time.

**Task 2 — List only the available books.**
Go through all returned books, but skip any that are marked as reserved. Print only the ones that are free to borrow.

Both tasks involve loops — but they stop or skip in different ways. This is what `break` and `continue` are for.

## What to Build

You have this list of returned books:

```
books = [
    {"title": "Sapiens",         "status": "available"},
    {"title": "1984",            "status": "reserved"},
    {"title": "The Alchemist",   "status": "damaged"},
    {"title": "Dune",            "status": "available"},
    {"title": "Ikigai",          "status": "reserved"},
    {"title": "Atomic Habits",   "status": "available"},
]
```

### Task 1 output — stop at first damaged

```
Checking: Sapiens
Checking: 1984
Checking: The Alchemist
Damaged book found: The Alchemist
Stopped checking.
```

### Task 2 output — skip reserved books

```
Sapiens — available
(skipping 1984, reserved)
The Alchemist — available
Dune — available
(skipping Ikigai, reserved)
Atomic Habits — available
```

## Topics You Will Need

- `for` loop — to go through each book in the list
- `break` — to exit the loop immediately when a condition is met
- `continue` — to skip the current item and move to the next one
- Dictionary access — `book["title"]`, `book["status"]`

## Before You Start — Think About This

1. `break` exits the loop entirely. `continue` only skips the current iteration and moves to the next. Which one does Task 1 need? Which one does Task 2 need?
2. After a `break`, does the code below the loop still run? Write a small experiment to find out.
3. After a `continue`, does the rest of the loop body for that iteration run? What gets skipped?
4. What if no damaged book exists in Task 1? How does your program handle that — what does it print?

## When You're Stuck

- `break` is used inside an `if` statement inside the loop: "if this condition is true, stop the loop entirely."
- `continue` is used similarly: "if this condition is true, skip the rest of this iteration and go back to the top of the loop."
- For Task 1, you may want to print a message after the loop finishes if no damaged book was found. Python's `for...else` construct handles this — look it up.

## Once It Works — Go Further

1. Combine both tasks: skip reserved books, but stop the moment you find a damaged one. What does that logic look like?
2. The librarian wants to know how many books were checked before the damaged one was found. Add a counter and print it.
3. Add a third status: `"missing"`. A missing book should stop the search immediately, just like a damaged one, but with a different message.
