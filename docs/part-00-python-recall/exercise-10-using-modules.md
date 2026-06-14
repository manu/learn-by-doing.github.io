---
title: "0.10 Using Modules"
parent: Python Recall Bootcamp
nav_order: 10
---

# Exercise 0.10 — Using Modules

## The Story

The library program is getting more useful. But you keep running into the same problem: Python knows how to do arithmetic, but it does not know what today's date is. It cannot pick a random book. It cannot calculate a square root without you writing the formula yourself.

You could write all of this from scratch. But someone already has.

Python comes with a large collection of ready-made tools called *modules*. Each module solves a specific category of problems. Instead of writing the solution, you *import* the module and use what is already there.

The librarian has two new requests:

1. "Every morning, show me a random book recommendation from the catalog — something different each time."
2. "When a student borrows a book, tell them the exact date it is due back — 14 days from today."

Both of these need modules you have never used before.

## What to Build

### Part 1 — Daily book recommendation

Your program should load the books from `books.csv` and pick one at random to recommend each time it runs.

```
--- Today's Recommendation ---
Read this: The Kite Runner by Khaled Hosseini (2003)
```

Run it again — a different book should appear.

### Part 2 — Due date calculator

Your program should ask when a book was borrowed and calculate the due date (14 days later). If today is the borrowed date, calculate from today.

```
Borrowed today? (y/n): y
Book borrowed on: 2026-06-14
Due back by:      2026-06-28
```

### Part 3 — Overdue checker

Given a due date, check whether the book is overdue and by how many days.

```
Enter due date (YYYY-MM-DD): 2026-06-01
This book is OVERDUE by 13 days.
Fine: Rs. 13.00 (Rs. 1 per day)
```

## Topics You Will Need

- `import random` — for picking randomly
  - `random.choice(list)` — pick one item from a list
- `import datetime` — for working with dates
  - `datetime.date.today()` — today's date
  - `datetime.timedelta(days=14)` — a duration of 14 days
  - `datetime.date.fromisoformat("2026-06-14")` — convert a string to a date
- The difference between a *date string* (`"2026-06-14"`) and a *date object* — you can do arithmetic on one but not the other

## Before You Start — Think About This

1. What does `import` actually do? Where does Python look for a module when you write `import random`?
2. `datetime.date.today()` returns an object, not a string. What can you do with a date object that you cannot do with a string?
3. If you write `import datetime` and then use `datetime.date.today()`, you are saying "in the `datetime` module, find the `date` class, then call `today()`". What does `from datetime import date` change about how you would call the same thing?
4. Two dates can be subtracted from each other. What do you get? Is it a number of days, or something else?

## When You're Stuck

- After `import random`, you call functions with `random.function_name()` — the module name comes first.
- After `from datetime import date`, you can write `date.today()` directly without the module prefix. Both styles work — understand what each one does.
- Subtracting two date objects gives a `timedelta` object. To get the number of days as an integer, use `.days` on the result.
- To check if a book is overdue: subtract the due date from today. If the result is positive (more than 0 days), it is overdue.

## Once It Works — Go Further

1. Look up `import math`. Use `math.sqrt()` in the prime checker from Exercise 0.8 instead of computing the square root yourself. How does this change the code?
2. Look up `import os`. Use `os.path.exists("books.csv")` to check whether the file exists before trying to open it — and print a helpful message if it does not.
3. The `random` module has more than `choice()`. Look up `random.sample()` and `random.shuffle()`. What are they useful for in a library context?
