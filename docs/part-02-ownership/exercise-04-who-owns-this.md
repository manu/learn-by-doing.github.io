---
title: "2.4 Who Owns This?"
parent: Ownership and Responsibility
nav_order: 4
---

# Exercise 2.4 — Who Owns This?

## The Story

A city library has thousands of books. No single staff member owns all the books — but there is a clear rule: **the cataloguing department is the only place where a book can be added, removed, or reclassified**. Other departments can look at the catalogue. They can request changes. But they cannot walk into the storeroom and move books themselves.

This rule exists because when anyone can change anything, nobody knows the current state of anything. The cataloguing department is the **owner** of the collection.

Now look at your Mini Library. Which function is the cataloguing department? Can any function add or remove books directly? If the answer is yes, you have no owner — you have chaos waiting to happen.

**Ownership** means: for every important piece of data, exactly one part of the program is responsible for it. Everyone else asks that owner for what they need.

## What to Do

### Part A — Assign owners

For each piece of data in your Mini Library, decide who owns it:

| Data | Who should be the only part of the program allowed to modify it? |
|------|------------------------------------------------------------------|
| The list of books | ? |
| An individual book's details | ? |
| The contents of the CSV file | ? |
| The search history (if you have it) | ? |
| The total count of books | ? |

Write your answer as a function name — the one function that is allowed to change this data. Then ask: does your current program enforce this, or can other functions bypass it?

### Part B — The borrowing contract

In a real library, staff don't go to the shelf themselves — they make a request. Design a "contract" for the books list:

Write three functions (just their names, parameters, and what they return — no code yet):
1. A function that adds a book and returns the updated collection
2. A function that removes a book by title and returns the updated collection
3. A function that returns all books without modifying anything

These three functions are the only way to interact with the books list. Nothing else in the program touches the list directly.

### Part C — Enforce the contract

Rewrite your Mini Library so that:
- All changes to the books list go through the three functions you designed
- No other function receives the books list and modifies it
- The main loop only calls these three functions — it does not manipulate the list itself

Test that the program behaves identically after the rewrite.

### Part D — What you just built

What you built in Part C has a name: it is called an **interface**. Other parts of the program do not need to know how the books are stored (list, dictionary, database) — they only need to know the contract: what functions are available and what they return.

Answer this: if you later changed the books list to a dictionary indexed by title (for faster searching), how many places in your program would you need to change?

Before Part C: count every place that touches the list directly.  
After Part C: count only the three functions you wrote.

The difference is the benefit of ownership.

## Topics You Will Learn

- The concept of data ownership — one responsible party per piece of data
- How to design a simple interface (a set of functions that are the only way to interact with data)
- Why ownership makes programs easier to change — change in one place, not many
- The early idea behind classes and objects (which will come much later in this curriculum)

## Before You Start — Think About This

1. In your current Mini Library, if you wanted to change from storing books in a CSV to storing them in a database, how many functions would you have to rewrite?
2. The total count of books is derived from the list — it is `len(books)`. Should it be a separate piece of data with its own owner, or should it always be calculated from the list? What is the risk of storing it separately?
3. Ownership is a discipline, not a Python feature. Python does not prevent you from modifying a list you should not touch. What does that tell you about the role of engineering judgment vs language rules?

## When You're Stuck

- Start by finding every line in your program that does `books.append(...)`, `books.remove(...)`, or `books.sort()` or similar. Each of those lines is a potential ownership violation.
- The "interface" you are building is just three regular Python functions. There is no new syntax to learn. The discipline is in deciding that *only those functions* are allowed to modify the data.
- If you are not sure whether a function should be allowed to modify the books list, ask: "Is this function's job to manage the collection, or is it doing something else (displaying, searching, exporting)?"

## Once It Works — Go Further

1. You built an interface using plain functions. Python classes do the same thing more formally — they bundle data and its allowed operations together. Research what a Python class looks like. You do not need to use classes yet — just understand that what you built is the idea behind them.
2. What happens if the function that adds a book also writes to the CSV? Is writing to the CSV part of "owning the books list" or is it a separate responsibility? Who should own the file?
