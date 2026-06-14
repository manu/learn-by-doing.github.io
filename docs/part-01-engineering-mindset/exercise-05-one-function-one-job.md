---
title: "1.5 One Function, One Job"
parent: Engineering Mindset
nav_order: 5
---

# Exercise 1.5 — One Function, One Job

## The Story

A librarian at a large city library gets a phone call:

> "I'd like to borrow a book, renew two others, report a damaged copy, pay a fine from last month, and also update my address."

The librarian puts the caller on hold, handles each of these one at a time with different systems, and calls back when done.

Now imagine if one single form handled all of this at once — borrow, renew, damage report, fine payment, address update — in one go. Nobody would know how to fill it in. Nobody would know what went wrong when it failed.

Functions in code work the same way. A function that does five things is hard to name, hard to test, hard to change, and hard to understand. A function that does one thing is easy to name, easy to test, easy to change, and easy to understand.

## The Problem

Here is what a Mini Library function might look like after a few months of "just add it here":

```
Input: book title, author, year, username
Output: prints confirmation message

Steps the function takes:
1. Checks if the title is already in the library
2. If a duplicate, prints "Already exists" and returns
3. Validates the year (must be a number, must be between 1900 and today)
4. Converts the year to an integer if it is a string
5. Adds the book to the in-memory list
6. Writes the updated list back to the CSV file
7. Logs the action with a timestamp to activity.log
8. Prints "Book added: [title]"
```

This function is doing seven different things. Can you name it with one phrase? Try. Any single name you give it will either be wrong, or so vague it tells you nothing.

## What to Do

### Part A — Break up the function

Take the function description above (not the code — you are designing the structure). Write the names of smaller functions that each do one job. For each function you design, write:
- The function name
- What it takes as input
- What it returns
- What it does (one sentence)

There is no single correct answer. The goal is for each function to be describable in one short sentence without the word "and".

### Part B — Apply this to your Mini Library

Open your `library.py`. Find any function that does more than one thing. You will recognize them because:
- They are longer than 20 lines
- Their name contains "and" (like `add_and_save`)
- You cannot describe what they do without multiple sentences
- They have sections separated by blank lines and comments

For each such function, write out a plan (on paper or in a comment) for how you would split it. Do not rewrite the code yet — only write the plan.

### Part C — Rewrite one

Pick the worst offender. Split it into smaller functions. Test that the program still behaves exactly the same after the split. You have not added features — you have only reorganized.

## Topics You Will Learn

- Single Responsibility Principle (one function, one job)
- How to identify when a function is doing too much
- Why small functions are easier to name, test, and change
- The difference between *refactoring* (changing structure) and *adding features* (changing behavior)

## Before You Start — Think About This

1. If a function is 5 lines, is it always doing one thing? Can a 5-line function still do two things? Give an example.
2. When you split one large function into five smaller ones, the total amount of code usually gets *longer*. Is that a problem?
3. A function named `process_book()` could do almost anything. A function named `validate_publication_year()` tells you exactly what it does. How does the name of a function signal whether it is doing one job or many?

## When You're Stuck

- If you cannot name a function in one phrase without using "and", it is doing more than one job.
- Start by drawing a list of what the function does, step by step. Then group steps that naturally belong together.
- A good test: can you test each new function independently, without needing to run the whole program?

## Once It Works — Go Further

1. After splitting the function, run your program and test it fully. Did any behavior change? If so, which change was a bug in your refactoring, and which was a bug that was already there?
2. Try naming each function you created using only a verb and a noun: `validate_year`, `save_to_csv`, `log_action`. Does that naming pattern work for all of them?
