---
title: "5.3 The 100,000 Book Problem"
parent: Real Data
nav_order: 3
---

# Exercise 5.3 — The 100,000 Book Problem

## The Story

You now have measurements. You know how slow the program is. You know which part is the bottleneck. Now the question is: why, fundamentally, is it slow — and is the problem solvable within the current architecture?

The answer, as you will discover, is no. The CSV-based library has hit its ceiling. No amount of Python optimisation will make a linear scan of 100,000 records fast enough for real use. The architecture itself needs to change.

This exercise is about arriving at that conclusion through reasoning, not through being told.

## What to Do

### Step 1 — Analyse the current search algorithm

Write down, in plain English, exactly what your `search_books()` function does when given a query:

1. Start at the first book in the list
2. Check if the query appears in the title
3. If yes, add it to the results
4. Move to the next book
5. Repeat until all books have been checked

Now count: with 100,000 books, how many comparisons does a single search require in the worst case (query matches no book)?

### Step 2 — Think about whether you can make it faster

Without changing the architecture (still using a list, still reading from CSV), explore whether any of these approaches help:

- **Sort the list on startup**: Can a sorted list be searched faster than an unsorted one? Try it. Measure it.
- **Limit search results early**: Stop after finding 20 matches instead of scanning the whole list. Does this help for common queries?
- **Cache the results**: If the same query is run twice, return the cached answer. Measure whether this matters for repeated searches.

For each approach, measure the effect. Write down: did it help? By how much?

### Step 3 — Identify what the CSV architecture cannot solve

After your experiments, write down three fundamental limitations of the current approach that cannot be fixed with Python code optimisation:

1. (Hint: what happens to memory as data grows to millions of books?)
2. (Hint: what happens if two people try to update the library at the same time?)
3. (Hint: what if you want to find all books borrowed by a specific member?)

### Step 4 — State the requirement for a better tool

Based on your analysis, write a one-paragraph description of what a better storage system would need to do. Do not mention SQL yet — just describe the capability you need. This is the problem statement that Part 6 will solve.

## Topics You Will Learn

- Linear search and why it does not scale
- The concept of an architectural ceiling — a limit that cannot be optimised past
- How to arrive at a technology decision through reasoning from evidence
- Writing a problem statement as a prerequisite to choosing a tool

## Before You Start — Think About This

1. A search through 100,000 books that checks each one takes 100,000 operations. If each operation takes 0.000001 seconds, total search time is 0.1 seconds. That sounds fast — but what if there are 100 users searching simultaneously? What if there are 10,000 users?
2. Is the CSV file's bottleneck the disk read (loading the data) or the computation (scanning the list)? Or both? How would you tell them apart?
3. If you were designing a tool specifically to make "find all books containing the word 'mystery'" fast — what would that tool look like internally? (This is how database indexes work — you are reinventing the concept.)

## When You're Stuck

- Binary search on a sorted list is dramatically faster than linear search — `O(log n)` instead of `O(n)`. But it only works for exact matches, not partial title matches. Why?
- The fundamental problem is not Python's speed — it is the algorithm. A faster language running the same algorithm would have the same scaling problem.
- Think about what information a dictionary (Python dict) or a hash table provides that a list does not. Could you build a structure that makes lookup faster?

## Transition to Part 6

You have now experienced the limits of the CSV approach. You can measure them precisely. You understand *why* they exist — not just that the program is slow, but which algorithmic property causes the slowness.

Part 6 introduces a tool built specifically to solve these problems. Before you start Part 6, write your answer to this question: **what would the ideal storage system do that CSV cannot?**

Your answer is the motivation for everything in Part 6.
