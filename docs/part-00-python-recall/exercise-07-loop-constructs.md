---
title: "0.7 Shelf Reports"
parent: Python Recall Bootcamp
nav_order: 7
---

# Exercise 0.7 — Shelf Reports

## The Story

The library has 5 shelves. Each shelf holds 8 books. The librarian wants three reports printed at the end of each week:

1. A numbered list of all shelf positions (Shelf 1 to Shelf 5, each with 8 slots)
2. A simple multiplication table showing how many books fit across different shelf and row combinations
3. A countdown from the last shelf to the first (for end-of-day reverse check)

You already know `while` loops. This exercise introduces the `for` loop and `range()` — the natural way to repeat something a fixed number of times — and nested loops, where one loop runs inside another.

## What to Build

### Report 1 — Shelf positions

```
Shelf 1: Slot 1, Slot 2, Slot 3, Slot 4, Slot 5, Slot 6, Slot 7, Slot 8
Shelf 2: Slot 1, Slot 2, Slot 3, Slot 4, Slot 5, Slot 6, Slot 7, Slot 8
Shelf 3: Slot 1, Slot 2, Slot 3, Slot 4, Slot 5, Slot 6, Slot 7, Slot 8
Shelf 4: Slot 1, Slot 2, Slot 3, Slot 4, Slot 5, Slot 6, Slot 7, Slot 8
Shelf 5: Slot 1, Slot 2, Slot 3, Slot 4, Slot 5, Slot 6, Slot 7, Slot 8
```

### Report 2 — Capacity grid (shelves 1–5, rows 1–4)

```
Shelves: 1  |  Rows: 1  |  Books: 8
Shelves: 1  |  Rows: 2  |  Books: 16
Shelves: 1  |  Rows: 3  |  Books: 24
Shelves: 1  |  Rows: 4  |  Books: 32
Shelves: 2  |  Rows: 1  |  Books: 16
...
Shelves: 5  |  Rows: 4  |  Books: 160
```

### Report 3 — Reverse countdown

```
Checking shelf 5...
Checking shelf 4...
Checking shelf 3...
Checking shelf 2...
Checking shelf 1...
Done.
```

## Topics You Will Need

- `for` loop with `range()` — repeat a fixed number of times
- `range(start, stop)` and `range(start, stop, step)` — control where the loop begins, ends, and how it steps
- Nested loops — a loop inside a loop; the inner loop completes fully before the outer loop moves to the next value
- `print()` with `end=` — to print on the same line without a newline

## Before You Start — Think About This

1. `range(1, 6)` gives you 1, 2, 3, 4, 5 — it stops *before* 6. Why do you think Python works this way?
2. Report 1 requires a loop inside a loop — one for shelves, one for slots. In what order do the two loops run? Which is the outer loop and which is the inner?
3. For Report 3, the numbers go from 5 down to 1. Can `range()` count backwards? What would you pass to it?
4. How many total iterations does Report 2 require? (Count the outer loop × inner loop.)

## When You're Stuck

- `for i in range(1, 6):` gives you `i` = 1, 2, 3, 4, 5.
- To count down: `range(5, 0, -1)` gives 5, 4, 3, 2, 1. The third argument is the step.
- For nested loops: write the outer loop first and get it printing one line, then replace that one line with an inner loop.
- To print without moving to the next line: use `print("Slot 1", end=", ")`. To move to the next line after the inner loop: use `print()` with no arguments.

## Once It Works — Go Further

1. Let the librarian enter the number of shelves and slots per shelf. The program generates the correct grid for any size.
2. Report 2 shows every combination. Modify it to only show combinations where the total book count is a multiple of 10.
3. Print Report 1 as a grid — shelves as rows, slot numbers as column headers — like a seating chart.
