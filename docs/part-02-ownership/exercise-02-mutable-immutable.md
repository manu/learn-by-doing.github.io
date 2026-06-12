---
title: "2.2 Mutable and Immutable"
parent: Ownership and Responsibility
nav_order: 2
---

# Exercise 2.2 — Mutable and Immutable

## The Story

Two engineers are working on the same library system. Engineer A passes a list of books to a function. Engineer B's function modifies the list to remove duplicates. Engineer A did not know that passing the list meant Engineer B's function could change it. Now Engineer A's data is different — and neither of them has any idea why.

This is one of the most common sources of bugs in programs with more than one function. It happens because in Python, some types of data can be changed *in place* (mutable) and some cannot (immutable). When you pass a mutable object to a function, the function can modify the original without returning anything — and without the caller knowing.

Understanding this is the difference between code that is predictable and code that surprises you.

## What to Do

### Part A — Observe the difference

Run each of these experiments in a Python file and write down exactly what you observe:

**Experiment 1:**
Start with `name = "Amal"`. Pass `name` to a function that tries to change it. Print `name` after the function returns. Did it change?

**Experiment 2:**
Start with `books = ["Sapiens", "1984"]`. Pass `books` to a function that appends a new title to it. Print `books` after the function returns. Did it change?

**Experiment 3:**
Start with `books = ["Sapiens", "1984"]`. Pass `books` to a function that does `books = books + ["new title"]` (reassignment, not append). Print `books` after the function returns. Did it change? Why is this different from Experiment 2?

### Part B — Fix the library

Here is the bug: the library's `remove_overdue()` function is supposed to return a cleaned list without modifying the original. But it modifies the original instead.

Write a version of `remove_overdue()` that:
- Takes a list of books as input
- Returns a new list with overdue books removed
- Does NOT modify the original list

Verify this by printing the original list before and after calling the function — it must be identical.

### Part C — Write a rule

After completing Parts A and B, write one sentence that explains when you should modify a list in place and when you should return a new list. This is your rule. You will apply it in every function you write from here on.

## Topics You Will Learn

- Mutable types (lists, dictionaries) vs immutable types (strings, numbers, tuples)
- The difference between mutating an object and reassigning a variable
- Why functions that modify their arguments are harder to reason about
- How to return a new object instead of modifying the original

## Before You Start — Think About This

1. When you pass a variable to a function in Python, does Python copy the value or pass a reference to the original? Does the answer depend on the type?
2. If a function modifies a list that was passed to it, is that modification visible to the caller? How would you test this?
3. What is the difference between `my_list.append(item)` and `my_list = my_list + [item]`? One mutates, one reassigns. Which is which?
4. Python has a type called `tuple` that looks like a list but cannot be modified. Why would you ever want a list that cannot be changed?

## When You're Stuck

- To create a copy of a list so you can modify it without affecting the original, use `new_list = original_list.copy()` or `new_list = list(original_list)`.
- Think of it this way: a variable is a label on a box. Two variables can have labels on the *same* box. Modifying the contents of the box affects everyone who has a label on it.
- If you are not sure whether a function is modifying its input, add a print statement before and after the function call to check.

## Once It Works — Go Further

1. Python's `tuple` is an immutable list. Convert the list of books in your Mini Library to a tuple and observe which operations stop working. When would a tuple be the right choice?
2. Dictionaries are also mutable. Write an experiment that shows how passing a dictionary to a function can silently modify the original, and then fix it using `.copy()`.
