---
title: "2.5 Pure Functions"
parent: Ownership and Responsibility
nav_order: 5
---

# Exercise 2.5 — Pure Functions and Side Effects

## The Story

The library runs a weekly statistics report. The `generate_report()` function calculates how many books were added this week, the most popular genre, and the average age of books in the collection.

One day, someone notices that calling `generate_report()` is *deleting the temporary log file*. The cleanup step was added quietly months ago — "it seemed related." Now every time anyone calls `generate_report()`, the log is wiped.

Nobody expected this. Nothing in the function's name suggested it. No documentation mentioned it.

This is a **side effect** — something a function does beyond what its name and purpose describe. Side effects are not always wrong. Writing to a file, printing to the screen, and saving to a database are all side effects — and they are necessary. The problem is *unexpected* side effects, where a function does something the caller did not know about.

The opposite of a function with side effects is a **pure function**: a function that, given the same input, always returns the same output and does nothing else. It does not print. It does not write files. It does not modify any data outside itself.

## What to Do

### Part A — Classify your functions

Go through every function in your Mini Library. For each one, classify it:

**Pure?** — Takes inputs, returns output, does nothing else. Call it a hundred times with the same input and get the same output each time.

**Side effects only?** — Prints to screen, writes to file, gets input from user. Does not return a meaningful value.

**Mixed?** — Does calculation AND has side effects. These are the ones to watch.

Write the classification next to each function name. Be honest — if a function both calculates something and prints it, it is mixed.

### Part B — The problem with mixed functions

Here is a mixed function:

```
Function: search_and_display(books, query)
- Filters books by query (calculation)
- Prints the results (side effect)
- Returns the count of results (output)
```

Why is this a problem? Try to answer these questions:

1. You want to use the search result in another function — to check if a book exists before adding a duplicate. Can you call `search_and_display()` without printing to the screen?
2. You want to test whether the search works correctly. To test it, you have to look at the printed output rather than check a return value. Is that easy to automate?
3. If you decide the results should be displayed differently (in a table instead of a list), how many things does this function do that you have to untangle?

### Part C — Separate calculation from action

For every "mixed" function you identified, split it into two:

- A **pure function** that does the calculation and returns the result
- An **action function** that calls the pure function and does something with the result (prints, saves, etc.)

Example:

```
Before: search_and_display(books, query)
After:  search_books(books, query) → returns list of matching books
        display_results(results) → prints them
```

The main program calls `display_results(search_books(books, query))`.

Apply this split to every mixed function you found.

### Part D — The test

After the split, verify the pure functions by calling them directly with known input and checking the output. You should be able to test `search_books` by calling it with a list of five books and a query — no printing, no files, just a return value you can inspect.

Write three such tests for your pure functions.

## Topics You Will Learn

- What a pure function is: same input → same output, no side effects
- What a side effect is: anything a function does beyond returning a value
- Why mixed functions are harder to reuse, test, and change
- The pattern of separating calculation (pure) from action (side effects)

## Before You Start — Think About This

1. `print()` is a side effect — it does something outside the function. Does that make every function that uses `print()` impure? Is that a problem?
2. A function that reads the current time (`datetime.now()`) cannot be pure — the same inputs give different outputs depending on when you call it. What other things make a function inherently impure?
3. If a function is pure, can you call it any number of times in any order without changing the program's behavior? Why does that matter?

## When You're Stuck

- The test for purity: can you call this function without the rest of the program, give it some inputs, and check its output? If yes, it is pure (or close to it).
- Start with the functions that calculate something — `count_books()`, `search_books()`, `find_overdue()`. These are the easiest to make pure.
- A function that calls `input()` is impure — it depends on what the user types. Move `input()` calls to the edge of your program (the main loop) and pass the values in as parameters.

## Once It Works — Go Further

1. After splitting your functions, count how many are pure vs action-only vs mixed. Has the number of mixed functions gone to zero?
2. Pure functions are very easy to test automatically. In Part 4 of this curriculum, you will write automated tests. Pure functions make that task much simpler. Keep note of which functions you made pure — you will return to them.
